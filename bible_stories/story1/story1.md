# Nuttig is mijn naam, onzeker mijn bestaan.

![Story1](story1.png)

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

<div id="description">
    ## Description

    Onesimus in de brief van Paulus aan Filemon. Onesimus betekent nuttig en was een weg gelopen slaaf die, met een brief van Paulus, terug ging naar zijn meester Filemon.
</div>

[Pick a new card](../random.md)
