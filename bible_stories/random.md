# Random Page Selector

This page will redirect to a random page from the list below every time it is accessed.

## Pages List
- [Page 1](story1.md)

<script>
    // List of page links
    const pages = [
        "story1.md",
    ];

    // Select a random page
    const randomPage = pages[Math.floor(Math.random() * pages.length)];

    // Redirect to the random page
    window.location.href = randomPage;
</script>