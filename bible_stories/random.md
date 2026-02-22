<div id="story-container">
    <p style="text-align:center;">Loading random story...</p>
</div>

<script>
    let currentLang = 'nl';
    let currentStory = null;

    async function loadStories() {
        try {
            const response = await fetch('stories.json');
            const data = await response.json();
            
            if (!data.stories || data.stories.length === 0) {
                document.getElementById('story-container').innerHTML = '<p>No stories found.</p>';
                return;
            }

            // Check if a specific story is requested via URL parameter
            const urlParams = new URLSearchParams(window.location.search);
            const requestedStoryId = urlParams.get('story');
            
            if (requestedStoryId) {
                // Find the specific story by ID
                currentStory = data.stories.find(story => story.id === requestedStoryId);
                
                if (!currentStory) {
                    document.getElementById('story-container').innerHTML = `<p>Story "${requestedStoryId}" not found.</p>`;
                    return;
                }
            } else {
                // Filter out stories that are not yet included (included === false)
                const includedStories = data.stories.filter(story => story.included !== false);
                
                if (includedStories.length === 0) {
                    document.getElementById('story-container').innerHTML = '<p>No included stories found.</p>';
                    return;
                }

                // Pick a random story from included stories
                currentStory = includedStories[Math.floor(Math.random() * includedStories.length)];
            }
            
            renderStory();
        } catch (error) {
            console.error('Error loading stories:', error);
            document.getElementById('story-container').innerHTML = '<p>Error loading stories.</p>';
        }
    }

    function renderStory() {
        if (!currentStory) return;

        const translation = currentStory.translations[currentLang] || currentStory.translations['nl'] || Object.values(currentStory.translations)[0];
        const availableLanguages = Object.keys(currentStory.translations);

        const container = document.getElementById('story-container');
        container.innerHTML = `
            <div class="controls">
                ${availableLanguages.length > 1 ? 
                    '<div class="language-buttons">' +
                    availableLanguages.map(lang => 
                        `<button onclick="switchLanguage('${lang}')" class="lang-btn ${lang === currentLang ? 'active' : ''}">${lang.toUpperCase()}</button>`
                    ).join('') +
                    '</div>'
                : ''}
            </div>

            <div class="riddle">
                <pre>${translation.title}</pre>
            </div>

            <div class="card" id="card">
                <div class="card-inner" id="card-inner">
                    <div class="card-front">
                        <img src="${currentStory.image}" alt="${translation.title}">
                    </div>
                    <div class="card-back">
                        <div class="answer">
                            <pre>${translation.description}</pre>
                            ${translation.reference ? `<div class="reference">${translation.reference}</div>` : ''}
                        </div>
                    </div>
                </div>
            </div>

            <div class="controls">
                <button onclick="location.reload()" class="new-card-btn">Pick a new card</button>
            </div>
        `;

        // Add triple-click flip functionality
        const card = document.getElementById('card-inner');
        let clickCount = 0;
        let clickTimer = null;
        
        card.addEventListener('click', function () {
            clickCount++;
            
            if (clickCount === 1) {
                clickTimer = setTimeout(function() {
                    clickCount = 0;
                }, 500);
            } else if (clickCount === 3) {
                clearTimeout(clickTimer);
                clickCount = 0;
                card.classList.toggle('flipped');
            }
        });
    }

    function switchLanguage(lang) {
        currentLang = lang;
        renderStory();
    }

    document.addEventListener('DOMContentLoaded', loadStories);
</script>

<style>
body {
    margin: 0;
    padding: 1rem;
}

#story-container {
    max-width: 600px;
    margin: 0 auto;
}

.controls {
    text-align: center;
    margin: 1rem 0;
}

.language-buttons {
    display: inline-flex;
    gap: 0.5rem;
}

.lang-btn {
    padding: 0.5rem 1rem;
    border: 2px solid #0366d6;
    background: white;
    color: #0366d6;
    border-radius: 5px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.2s;
}

.lang-btn:hover {
    background: #f0f8ff;
}

.lang-btn.active {
    background: #0366d6;
    color: white;
}

.riddle {
    text-align: center;
    margin: 1.5rem 0;
}

.riddle pre {
    font-family: inherit;
    font-size: 1.1rem;
    white-space: pre-wrap;
    margin: 0;
    font-weight: 500;
}

.card {
    perspective: 1000px;
    margin: 2rem auto;
    max-width: 500px;
}

@media (max-width: 768px) {
    .card {
        max-width: 100%;
    }
}

.card-inner {
    position: relative;
    width: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    cursor: pointer;
}

.card-inner:hover {
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.card-front, .card-back {
    width: 100%;
    backface-visibility: hidden;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-front {
    position: relative;
}

.card-front img {
    width: 100%;
    height: auto;
    display: block;
}

@media (max-width: 768px) {
    .card-front img {
        object-fit: cover;
        min-height: 400px;
    }
}

.card-back {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform: rotateY(180deg);
    background: #f9f9f9;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    box-sizing: border-box;
}

.answer pre {
    font-family: inherit;
    font-style: italic;
    white-space: pre-wrap;
    text-align: center;
    margin: 0 0 1rem 0;
    font-size: 1rem;
}

.reference {
    text-align: center;
    font-weight: 600;
    color: #0366d6;
    margin-top: 1rem;
    font-size: 0.95rem;
}

.card-inner.flipped {
    transform: rotateY(180deg);
}

.new-card-btn {
    padding: 0.75rem 1.5rem;
    background: #0366d6;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 600;
    transition: background 0.2s;
}

.new-card-btn:hover {
    background: #0256c7;
}
</style>