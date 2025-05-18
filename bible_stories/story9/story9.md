# Het jeukte op mijn rug, nu sjokken mijn ezels wel erg langzaam terug

<div class="flip-container" style="width:100%;max-width:500px;margin:auto;">
    <div class="flipper" id="flipper">
        <div class="front">
            <img src="story9.png" alt="Story9" style="width:100%;height:auto;display:block;">
        </div>
        <div class="back" style="display:flex;align-items:center;justify-content:center;height:100%;background:#f9f9f9;">
            <div id="description" style="text-align:center;font-style:italic;padding:2em;">
                2 Koningen 5: Naaman, na zijn genezing, vraagt of hij aarde mee mag nemen
            </div>
        </div>
    </div>
</div>

<style>
.flip-container {
    perspective: 1000px;
}
.flipper {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 66.66%; /* 3:2 aspect ratio */
    transition: 0.6s;
    transform-style: preserve-3d;
}
.front, .back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    top: 0;
    left: 0;
}
.front {
    z-index: 2;
}
.back {
    transform: rotateY(180deg);
    z-index: 1;
}
.flipped {
    transform: rotateY(180deg);
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function () {
    const flipper = document.getElementById('flipper');
    flipper.addEventListener('dblclick', function () {
        flipper.classList.toggle('flipped');
    });
});
</script>

[Pick a new card](../random.md)
