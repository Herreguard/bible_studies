# Random Page Selector

This page will redirect to a random page from the list below every time it is accessed.

## Pages List
- [Story1](story1/story1.md)
- [Story2](story2/story2.md)
- [Story3](story3/story3.md)
- [Story4](story4/story4.md)
- [Story6](story6/story6.md)
- [Story7](story7/story7.md)
- [Story8](story8/story8.md)

<script>
    // List of page links
    const pages = [
        "story1/story1.html",
        "story2/story2.html",
        "story3/story3.html",
        "story4/story4.html",
        "story6/story6.html",
        "story7/story7.html",
        "story8/story8.html",
        "story9/story9.html"
    ];

    // Select a random page
    const randomPage = pages[Math.floor(Math.random() * pages.length)];

    // Redirect to the random page
    window.location.href = randomPage;
</script>