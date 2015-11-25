# Visualizacion-3d
efecto tridimensional  generado por movimientos en el eje z
//Active researchers by region, 2004 - 2013
//tabla 3.2.9. Investigadores activos vinculados a grupos por entidad territorial, 2004 – 2013*
PFont gluck;
PFont otraletra;
PFont letras;
PFont titulo; 
PFont  depar ;
PImage img;

Table barras;

int rcirculo=200;
int centrox=500;
int centroy=500;

float x1;
float y1;
float x2;
float y2;


//una sola vez
void setup()
{ 
  size(1000, 1000, P3D); 


  barras=loadTable("activos.csv"); 
  gluck = loadFont("AgencyFB-Bold-20.vlw"); 
  otraletra = loadFont("AgencyFB-Bold-15.vlw"); 
  otraletra = loadFont("AgencyFB-Bold-40.vlw");
  depar = loadFont("Arial-BoldMT-20.vlw");
}



// lo que se repite 

void draw() { 



  smooth(25);
  //circulo en el fondo 

  noFill();
  stroke(0);
  ellipse(500, 500, 750, 750);

  //fondo
  background(255, 255, 255, 85);

  //for para dibujar las lineas 


  for (int fila = 0; fila<28; fila=fila+1) {

    x1=centrox+(rcirculo*cos(fila*0.57119866428905)-barras.getInt(fila, 1)*cos(fila*0.57119866428905));
    y1=centroy+(rcirculo*sin(fila*0.57119866428905)-barras.getInt(fila, 1)*sin(fila*0.57119866428905));
    x2=centrox+rcirculo*cos(fila*0.57119866428905);
    y2=centroy+rcirculo*sin(fila*0.57119866428905);


    // ancho de las lineas
    strokeWeight(20);

    //cuando muevo el mouse hacia la derecha o izquierda se aleja en z

    translate(0, 0, mouseX);
    scale(1);


    strokeWeight(0.8); 
    stroke(45, 255, 255, 100);
    stroke(10); 

    noFill();
    ellipse(centrox, centroy, 400, 400);

    fill(255, 248, 18);
    ellipse(x1, y1, 5, 5);

    fill(18, 27, 255);
    ellipse(x1, y1, 3, 3);

    fill(255, 0, 0);
    ellipse(x1, y1, 1.5, 1.5);

    noFill();       
    strokeWeight(2); 
    stroke(0);
    line(x1, y1, x2, y2);

    fill(0);
    ellipse(x2, y2, 1.5, 1.5);




    noFill();

    //texto en las lineas 
    fill(0);

    textFont(otraletra, 30);
    //numeros al final de la linea
    text(barras.getString(fila, 1), x1+5, y1+5);

    //departamentos 
    String dep = barras.getString(fila, 0);
    if (fila == 5) { dep ="Bogotá"; 
    }
   

    
    
    text(dep, x2+10, y2+30);
  }
  for (int cub = 0; cub <= 1000; cub= cub+10) {
    for (int rub = 0; rub <= 1000; rub= rub+10) {
      noFill();
      strokeWeight(0.5);
      stroke(215, 200, 210, 100);
      rect(cub, rub, 10, 10);
    }
  }
  //circulos que decoran 
  noStroke();
  fill(255, 245, 255, 100);
  ellipse(centrox, centroy, 600, 600);

  noStroke();
  fill(245, 255, 255, 70);
  ellipse(centrox, centroy, 800, 800);

  noStroke();
  fill(255, 245, 245, 70);
  ellipse(centrox, centroy, 800, 800);
  //titulo de abajo 



  textFont(otraletra, 48);
  smooth(25);
  fill(0);
  text("Promedio de Investigadores Activos ", 50, 880);
  text("Según Unidad Regional ", 50, 930);

  textFont( gluck, 20);
  //numeros al final de la linea
  text("Average Number of Researchers by Regional Unit ", 50, 980);
}
