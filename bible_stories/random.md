# Random Page Selector

This page will redirect to a random page from the list below every time it is accessed.

## Pages List
- [Story1](story1/story1.md)
- [Story2](story2/story2.md)

<script>
    // List of page links
    const pages = [
        "story1/story1.md",
        "story2/story2.md",
    ];

    // Select a random page
    const randomPage = pages[Math.floor(Math.random() * pages.length)];

    // Redirect to the random page
    window.location.href = randomPage;
</script>