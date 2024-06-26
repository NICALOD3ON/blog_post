---
title: Week 6
published_at: 2024-04-1
snippet: First day in Creative Coding!
disable_html_sanitization: true
---

script tag - this leads to a file path. the '..' means go out of the current folder, to go into a different folder.

<script src="/scripts/cs.min.js"></script>
<canvas id="c2"/>

<script>
    //Created by Ren Yuan


const renderer = new c2.Renderer(document.getElementById('c2'));
resize();


renderer.background('#cccccc');
renderer.fontSize(12);
renderer.fontWeight('normal');
renderer.textAlign('left');
renderer.textBaseline('top');

let random = new c2.Random();
let color = c2.Color.hsl(random.next(0, 30), random.next(30, 60), 60);

let points = [];
for(let i=0; i<200; i++){
    let x = random.next(-renderer.width/2, renderer.width/2);
    let y = random.next(-renderer.height/2, renderer.height/2);
    points[i] = new c2.Point(x, y);
}


let a = 2, b = 1;
let f = (x) => a * x + b;
let classify = (x, y) => y < f(x) ? 0:1;


let neuralNet = new c2.NeuralNet(2, 1, 0, 0);
let n = neuralNet.weights().length;


function fitness(chromosome){
    let score = 0;

    neuralNet.weights(chromosome.genes);
    for (let i = 0; i < points.length; i++) {
        let p = points[i];
        let output = neuralNet.feedforward([p.x, p.y]);
        let answer = classify(p.x, p.y);
        if((output[0]<.5) == (answer==0)) score++;
    }
    
    chromosome.fitness = score/points.length;
}

let chromosomes = [];
for(let i=0; i<10; i++) {
    let c = new c2.Chromosome();
    c.initFloat(n, -1, 1);
    chromosomes.push(c);
}

let p = new c2.Population(chromosomes, .9, .01, fitness);
p.setSelection('tournament', 5);
p.setCrossover('two_point');
c2.Mutation.maxDeviation = .1;
p.setMutation('deviate');




renderer.draw(() => {
	renderer.clear();


	let info = p.fitness();
    let best = info.bestChromosome;
    neuralNet.weights(best.genes);
    let weights = neuralNet.weights();

    
    renderer.save();
    renderer.translate(renderer.width/2, renderer.height/2);

    let x1 = -renderer.width/2;
    let y1 = -(weights[2] + weights[0]*x1)/weights[1];
    let x2 = renderer.width/2;
    let y2 = -(weights[2] + weights[0]*x2)/weights[1];

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    renderer.fill(color);
    renderer.quad(x1, y1, x2, y2, renderer.width/2, renderer.height/2, renderer.width/2, -renderer.height/2);

    for (let i = 0; i < points.length; i++) {
        let p = points[i];

        renderer.stroke('#333333');
        renderer.fill(false);
        if(classify(p.x, p.y)<.5) {
            renderer.lineWidth(5);
            renderer.point(p);
            
        }else {
            renderer.lineWidth(2);
            renderer.circle(p.x, p.y, 3);
        }
    }

    renderer.restore();


    let tx = 20;
    let ty = 20;
    renderer.stroke(false);
    renderer.fill('#333333'); 
    renderer.text('generation ' + info.generation, tx, ty);
    renderer.text('best fitness ' + info.bestFitness.toFixed(2), tx, ty+15);
    renderer.text('worst fitness ' + info.worstFitness.toFixed(2), tx, ty+30);
    renderer.text('average fitness ' + info.averageFitness.toFixed(2), tx, ty+45);

    if(info.bestFitness != 1) p.reproduction();
});


window.addEventListener('resize', resize);
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>

code from [here] https://c2js.org/examples.html