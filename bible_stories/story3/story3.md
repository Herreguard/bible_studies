# Samen zijn we overdonderend

![Story3](story3.jpeg)

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
    Jacobes en Johannes. De gebroederes van de donder genoemd in Markus 3:17.
</div>

[Pick a new card](../random.md)
