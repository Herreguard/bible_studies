# Deze diepe bron uit verre streken, wordt tegenwoordig nog bekeken.

![Story15](story15.jpeg)

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
    Koning Hizkia bouwt een waterleiding van de Gihonbron naar de Siloambron binnen de stadsmuren van Jeruzalem. Dit is tegenwoordig een toeristische attractie (2 Kronieken 32:30; 2 Koningen 20:20; Jesaja 22:9-11).
</div>

[Pick a new card](../random.md)
