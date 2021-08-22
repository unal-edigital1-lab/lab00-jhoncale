@ -1,9 +1,30 @@
# lab01- sumador 



laboratorio 01 introducción a HDL

En esta plantilla debe adicionar la documentación del laboratorio

* Jhon Nelson Caceres Leal.
------------------------------------------------------------------------------------------------------------------

*En este primer apartado del laboratorio inicial, se configura el framework para FPGA

los fpga son dispositivos reconfigurables, en la cual se implementa logica combicional o secuencial 


#0 Descargar instaldor

1.primero se descarga los arcjhivos de instalacion y se ejecutan, una vez instalados se ejecuta y se prepara el primer proyecto 
2.se crea un nuevo archivo seleccionando el directorio y se configura el top

## EJERCICIO 1 Diseño de sumador 1 bit
### 1. se diseña un sumador de 1bit 

se diseña un sumador de un bitA completo y un bit B completo, el sumador cuenta con un carrier y se ejecuta segun la tabala de verdad entregada anteriormente 




```verilog

module sum1bcc (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;

  reg [1:0] st;

  assign S = st[0];
  assign Cout = st[1];

  always @ ( * ) begin
  	st  = 	A+B+Ci;
  end
  
endmodule

```

Se utilizan todas las posibles entradas para validar el simulador, para luego ejecutar el testBench, obteniendo todos los posibles valores




### 2. Bloque Funcional
Según la especificación del sumador completo de 1 bit. se deduce que el bloque o modulo funcional esta dado por:

```verilog
module sum1bcc_TB;

  reg x;
  reg y;
  reg c;
  wire out;
  wire z;


sum1bcc uut(x, y, c,out,z);


initial begin
forever begin
x=0; y=0; c=0; #3;
x=0; y=0; c=1; #3;
x=0; y=1; c=0; #3;
x=0; y=1; c=1; #3;
x=1; y=0; c=0; #3;
x=1; y=0; c=1; #3;
x=1; y=1; c=0; #3;
x=1; y=1; c=1; #3;
end


end

initial begin: TEST_CASE
     $dumpfile("sum1bcc_TB.vcd");
     $dumpvars(-1, uut);
     #(200) $finish;
   end

endmodule
```

### 3. implementacion 

En mi caso no tengo la placa, así que los pasos siguientes fueron realizados junto con mis compañeros de grupo que si tiene las tarjetas físicas. 

se asigna la targe a utilizar, luego se asignan los pines que se utilizaran para sintetizar el programa 

Luego se visualizan las conexiones entre los pines y las entradas lógicas

Por último se conecta la placa por medio del cable USB, instalando los certificados y driver.

![image](https://user-images.githubusercontent.com/38961990/130364397-374f5433-a640-4475-923f-0e0d9418de65.png)
