# L-System - Sistema de Lindenmayer

L-Systems são as estruturas e procedimentos criados por Aristide Lindenmayer para estudar o crescimento de algas e plantas, por meio da manipulação de sequências de símbolos. As sequências são geradas por sucessivas iterações da aplicação de regras de substituição. A tradução computacional dessas estruturas foi discutida pela primeira vez em *Lecture Notes in Biomathematics* por Przemyslaw Prusinkiewcz e James Hanan.

Referências externas:
- [The Algorithmic Beauty of Plants](http://algorithmicbotany.org/papers/#abop) (+ diversos livros e artigos)
- https://www.cgjennings.ca/articles/l-systems/
- http://www.paulbourke.net/fractals/lsys/ 

```python
axioma = 'X'
regras = {
    'X': 'F+[[X]-X]-F[-FX]+X',
    'F': 'FF',      
    }
passo = 5
angulo = 25 # angulo em graus
iteracoes = 5
tam = random(5, 10)


def setup():
    global frase_resultado
    size(900, 900, P3D)
    frase_inicial = axioma
    for _ in range(iteracoes):
        frase_resultado = ''
        for simbolo in frase_inicial:
            substituir = regras.get(simbolo, simbolo)
            frase_resultado = frase_resultado + substituir
        #print(frase_inicial, frase_resultado)
        frase_inicial = frase_resultado    
    print(len(frase_resultado))
    
def draw():
    background(200, 200, 150)
    randomSeed(2)
    strokeWeight(1) 
    for i in range(4):
        for j in range(4):
            if j % 2 == 0:
                x = 200 + i * 200
            else: 
                x = 100 + i * 200
            y = 200 + j * 200
            # plot(x, y, 5 + j * 10 -i * 3)
            plot(x, y + 50, random(10,25))
                   
def plot(x, y, angulo):    
        pushMatrix()
        translate(x, y)  
        scale(0.5)
        # angulo = 25
        # angulo = mouseX / 70.0
        # translate(width / 2, height * 0.8)
        rotateY(frameCount / 35.0)
        for simbolo in frase_resultado:
            if simbolo == 'X':   # se simbolo for igual a 'X'
                pass
            elif simbolo == 'F':   # else if (senão se) o simbolo é F
                    line(0, 0, 0, -passo)
                    translate(0, -passo)
                    rotateY(radians(-angulo))
            elif simbolo == '+':
                rotate(radians(-angulo)) # + random(-5, 5)))
            elif simbolo == '-':
                rotate(radians(+angulo)) # + random(-5, 5)))
            elif simbolo == '[':
                pushMatrix()
            elif simbolo == ']':    
                popMatrix()
        popMatrix()    
        
def keyPressed():
    if key == 's':
        saveFrame('imagem###.png') 

```
