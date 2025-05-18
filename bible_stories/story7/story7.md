# Ik was te vies om aan te zien, daarna werd ik een fris groen ding

![Story7](story7.png)

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
    2 Koningen 5: 14 - Naaman's huid veranderd in 'als die van een klein jongen (babyface) 
</div>

[Pick a new card](../random.md)
