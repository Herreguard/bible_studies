# Deze honderd mensen kunnen eten zoveel ze wensen

![Story11](story11.jpeg)

<style>
    img {
        width: 100%;
        height: auto;
    }
</style>

<script>
    document.addEventListener('DOMContentLoaded', function () {
        const img = document.querySelector('img');
        const description = document.querySelector('#description');
        description.style.display = 'none';

        img.addEventListener('dblclick', function () {
            if (description.style.display === 'none') {
                description.style.display = 'block';
            } else {
                description.style.display = 'none';
            }
        });
    });
</script>

<div id="description" style="text-align: center; font-style: italic;">
    2 Koningen 4:42-44: "Elia voedt honderd mensen met twintig gerstekorrelbroden en enkele gerstebroodjes."
</div>

[Pick a new card](../random.md)
