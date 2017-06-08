# SOLARIS
float xMove;
boolean flash = false;

Star[] stars= new Star[150];
int count=100;
float spin = 0;
float dist;
float []orbit=new float[9];

class Planet{
  float dist;
  float size;
  float speed;
  color StarColor;
  
  Planet(float dist, float size, float speed,color StarColor){
    this.dist = dist;
    this.size = size; 
    this.speed = speed;
    this.StarColor=StarColor;
  }
  
  void drawPlanet(float t){
    pushMatrix();    
    stroke(StarColor);
    rotateY(radians(0.1*speed*t));
    translate(dist, 0, 0);
    sphere(size);
    popMatrix();
  }
}

ArrayList solarSystem = new ArrayList();

void setup(){
  fullScreen(P3D); 
  stroke(255);
  noFill();
  sphereDetail(20);
  solarSystem.add(new Planet(0, 70, 0,color(255,255,0)));
  solarSystem.add(new Planet(100, 4, 100,color(100,255,255)));
  solarSystem.add(new Planet(120, 8, 80,color(255,200,0)));
  solarSystem.add(new Planet(150, 10, 60,color(0,100,200)));
  solarSystem.add(new Planet(180, 8, 40,color(255,0,0)));
  solarSystem.add(new Planet(280, 14,20,color(255,200,80)));
  solarSystem.add(new Planet(380, 13, 15,color(255,255,0)));
  solarSystem.add(new Planet(550, 8, 10,color(0,255,255)));
  solarSystem.add(new Planet(700, 8, 5,color(0,0,255)));
  orbit[1]=(200);
  orbit[2]=(240);
  orbit[3]=(300);
  orbit[4]=(360);
  orbit[5]=(560);
  orbit[6]=(760);
  orbit[7]=(1100);
  orbit[8]=(1400);  
  
  for(int i = 0; i < 150 ; i++){
    stars[i] = new Star(-800+10*random(width), -800+10*random(height),6, 4, count);
    count += 5;
  }
}

void draw(){
  background(0);
  translate(width/2, height/2-50, 0);
  rotateX(-radians(50));
  //rotateY(radians(10+ spin));
  for(Star star : stars){
      //stroke(255);
      star.shown();
      star.twinkle();
      star.move();
  }
  for(int i = 0; i < 9; i++){
    Planet p = (Planet) solarSystem.get(i);
    if(i!=0)path(orbit[i]);
    p.drawPlanet(spin);
  }
  spin = spin + 0.5; //this determines the rotation  
}

void path(float dist){
  stroke(255);
  pushMatrix();
  rotateX(PI/2);
  ellipseMode(CENTER);
  ellipse(0, 0, dist, dist);
  popMatrix();
}

class Star {
  boolean flash = false;
  float x, y;
  int w, h, c;
   
  Star(float xPos, float yPos, int largura, int altura, int contador){
    x = xPos;
    y = yPos;
    w = largura;
    h = altura;
    c = contador;
  }
  void twinkle() {
    stroke(random(0,255));
  } 
  void fallingStars(){     
    if(!flash && c % 30 == 0){
      fill(190, 190, 190);
      flash = !flash;
    }
    else if(flash && c % 30 == 0){
      fill(0);
      flash = !flash;
    }
    c += 5;     
  }
  void move(){
    y+=1;
    if( y > 740 )
      y = 0;
  }   
  void shown(){
    ellipse(x, y, w, h);
  }
}
