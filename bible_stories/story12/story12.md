# Ik werd voorgelezen in de nacht totdat ik aan een beloning dacht

![Story7](story7.jpeg)

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
    Esther 6:1-14: "Koning Ahasveros kan niet slapen en laat zich voorlezen uit de kronieken."
</div>

[Pick a new card](../random.md)
