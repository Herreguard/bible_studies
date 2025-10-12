# Als mijn man het niet zou weten, zou ik geen stof hebben gegeten

![Story7](story14.jpeg)

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
    Numeri 5:11-31: "Een vrouw moet een beker met stof drinken om haar onschuld te bewijzen."
</div>

[Pick a new card](../random.md)
