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

            // Pick a random story
            currentStory = data.stories[Math.floor(Math.random() * data.stories.length)];
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
            <div style="text-align:center;margin-bottom:1rem;">
                ${availableLanguages.length > 1 ? availableLanguages.map(lang => 
                    `<button onclick="switchLanguage('${lang}')" style="margin:0 0.5rem;padding:0.5rem 1rem;${lang === currentLang ? 'font-weight:bold;' : ''}">${lang.toUpperCase()}</button>`
                ).join('') : ''}
            </div>

            <h1 style="text-align:center;">${translation.title}</h1>

            <div class="flip-container" style="width:100%;max-width:500px;margin:auto;">
                <div class="flipper" id="flipper">
                    <div class="front">
                        <img src="${currentStory.image}" alt="${translation.title}" style="width:100%;height:auto;display:block;">
                    </div>
                    <div class="back" style="display:flex;align-items:center;justify-content:center;height:100%;background:#f9f9f9;">
                        <div id="description" style="text-align:center;font-style:italic;padding:2em;">
                            ${translation.description}
                        </div>
                    </div>
                </div>
            </div>

            <p style="text-align:center;margin-top:2rem;">
                <a href="random.md" onclick="location.reload(); return false;" style="padding:0.5rem 1rem;background:#0366d6;color:white;text-decoration:none;border-radius:5px;">Pick a new card</a>
            </p>
        `;

        // Add flip functionality
        const flipper = document.getElementById('flipper');
        flipper.addEventListener('dblclick', function () {
            flipper.classList.toggle('flipped');
        });
    }

    function switchLanguage(lang) {
        currentLang = lang;
        renderStory();
    }

    document.addEventListener('DOMContentLoaded', loadStories);
</script>

<style>
.flip-container {
    perspective: 1000px;
}
.flipper {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 66.66%; /* 3:2 aspect ratio */
    transition: 0.6s;
    transform-style: preserve-3d;
}
.front, .back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    top: 0;
    left: 0;
}
.front {
    z-index: 2;
}
.back {
    transform: rotateY(180deg);
    z-index: 1;
}
.flipped {
    transform: rotateY(180deg);
}
</style>