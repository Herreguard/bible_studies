# Bij het controleren van mijn cassette, miste ik mijn laatste set

![Story16](story16.jpeg)

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
    Ezra 1: 9 : Er mist een mes bij het set van dertig gouden schalen en bekers die teruggebracht zijn uit Babel.
</div>

[Pick a new card](../random.md)
