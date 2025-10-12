# Random Page Selector

This page will redirect to a random page from the list below every time it is accessed.

## Pages List
<ul id="story-list">
    <li>Loading stories…</li>
</ul>

<script>
    async function resourceExists(url) {
        try {
            const headResponse = await fetch(url, { method: 'HEAD', cache: 'no-store' });
            if (headResponse.ok) {
                return true;
            }
            if (headResponse.status === 405) {
                const getResponse = await fetch(url, { method: 'GET', cache: 'no-store' });
                return getResponse.ok;
            }
        } catch (error) {
            console.warn(`Unable to reach ${url}:`, error);
        }
        return false;
    }

    async function discoverStory(index) {
        const storyId = `story${index}`;
        const basePath = `${storyId}/${storyId}`;

        const htmlUrl = `${basePath}.html`;
        const mdUrl = `${basePath}.md`;
        const jpegUrl = `${basePath}.jpeg`;
        const pngUrl = `${basePath}.png`;

        const [hasHtml, hasMd, hasJpeg, hasPng] = await Promise.all([
            resourceExists(htmlUrl),
            resourceExists(mdUrl),
            resourceExists(jpegUrl),
            resourceExists(pngUrl)
        ]);

        if (!hasHtml && !hasMd) {
            return null;
        }

        const preferredPage = hasHtml ? htmlUrl : mdUrl;
        const image = hasJpeg ? jpegUrl : (hasPng ? pngUrl : null);

        return {
            index,
            title: `Story ${index}`,
            pageUrl: preferredPage,
            mdUrl: hasMd ? mdUrl : null,
            imageUrl: image
        };
    }

    function buildListItem(story) {
        const listItem = document.createElement('li');

        const mainLink = document.createElement('a');
        mainLink.href = story.pageUrl;
        mainLink.textContent = story.title;
        listItem.appendChild(mainLink);

        if (story.mdUrl && story.mdUrl !== story.pageUrl) {
            const mdLink = document.createElement('a');
            mdLink.href = story.mdUrl;
            mdLink.textContent = 'Markdown';
            mdLink.style.marginLeft = '0.5rem';
            listItem.appendChild(document.createTextNode(' ('));
            listItem.appendChild(mdLink);
            listItem.appendChild(document.createTextNode(')'));
        }

        if (story.imageUrl) {
            const imageThumb = document.createElement('img');
            imageThumb.src = story.imageUrl;
            imageThumb.alt = `${story.title} preview`;
            imageThumb.loading = 'lazy';
            imageThumb.style.display = 'block';
            imageThumb.style.maxWidth = '200px';
            imageThumb.style.marginTop = '0.5rem';
            listItem.appendChild(imageThumb);
        }

        return listItem;
    }

    async function loadStories() {
        const storyList = document.getElementById('story-list');
        const stories = [];
        let consecutiveMisses = 0;
        const maxStories = 200;
        const missLimit = 10;

        for (let i = 1; i <= maxStories && consecutiveMisses < missLimit; i++) {
            const story = await discoverStory(i);
            if (story) {
                stories.push(story);
                consecutiveMisses = 0;
            } else {
                consecutiveMisses++;
            }
        }

        if (!stories.length) {
            storyList.innerHTML = '<li>No stories found yet.</li>';
            return;
        }

        stories.sort((a, b) => a.index - b.index);

        storyList.innerHTML = '';
        stories.map(buildListItem).forEach((item) => storyList.appendChild(item));

        const randomStory = stories[Math.floor(Math.random() * stories.length)];
        window.location.href = randomStory.pageUrl;
    }

    document.addEventListener('DOMContentLoaded', loadStories);
</script>