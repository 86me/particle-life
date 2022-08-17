# Particle Life Simulation
A simple program to simulate attraction/reuplsion forces between many particles

Learn More Here (video tutorial):
-----------------------------------------------
video tutorial comming soon

Interface
--------------------------------------------------------
![](images/interface.jpg)

Example Results
--------------------------------------------------------
![](images/big_pic.jpg)

Code
----------------
Source code available in both C++ (using openframeworks liberary) and javascript

The java script code is as simple as this:
```
<canvas id="life" width="500" height="500"></canvas>
<script>
m = document.getElementById("life").getContext('2d')
atoms = []
atom =  function(x, y, c){ 
  this.x = x 
  this.y = y
  this.vx = 0
  this.vy = 0
  this.color = c
}
draw = function(x, y, c, s){ 
  m.fillStyle = c
  m.fillRect(x, y, s, s)
}
random = function(){ return Math.random() * 400 + 50 }
create =  function(n, c){
  group = []
  for(let i=0; i<n; i++){
     group.push(new atom(random(), random(), c))
     atoms.push(group[i])
  }
  return group
}

rule = function(group1, group2, G){
  g = -0.01 * G
  for(i=0; i<group1.length; i++){
    fx = 0
    fy = 0
    a = group1[i]
    for(j=0; j<group2.length; j++){
      b = group2[j]
      dx = a.x-b.x
      dy = a.y-b.y
      d = Math.sqrt(dx*dx + dy*dy)
      if(d > 0 && d < 80){
        fx += dx/d
        fy += dy/d
      }
    }
    a.vx = (a.vx + (g * fx))*0.5
    a.vy = (a.vy + (g * fy))*0.5
    a.x += a.vx
    a.y += a.vy
    if(a.x < 0 || a.x > 500){ a.vx *=-1 }
    if(a.y < 0 || a.y > 500){ a.vy *=-1 }
  }
}
yellow = create(200, "yellow")
red = create(200, "red")
green = create(200, "green")
update = function(){
  rule(green, green, 32)
  rule(green, red, 17)
  rule(green, yellow, -34)
  rule(red, red, 10)
  rule(red, green, 34)
  rule(yellow, yellow, -15)
  rule(yellow, green, 20)
  m.clearRect(0, 0, 500, 500)
  draw(0, 0, "black", 500);
  for(i=0; i<atoms.length; i++){ 
    draw(atoms[i].x, atoms[i].y, atoms[i].color, 5) 
  }
  requestAnimationFrame(update);
}
update();
</script>
```

</br>
