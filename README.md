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
## Sumador de 4 Bits

Se usa el código para el sumador de 1 bit y sé instancia 4 veces 

```verilog

`timescale 1ns / 1ps
module sum4b(xi, yi,co,zi);


  input [3 :0] xi;
  input [3 :0] yi;
  output co;
  output [3 :0] zi;

  wire c1,c2,c3;
  sum1bcc s0 (.A(xi[0]), .B(yi[0]), .Ci(0),  .Cout(c1) ,.S(zi[0]));
  sum1bcc s1 (.A(xi[1]), .B(yi[1]), .Ci(c1), .Cout(c2) ,.S(zi[1]));
  sum1bcc s2 (.A(xi[2]), .B(yi[2]), .Ci(c2), .Cout(c3) ,.S(zi[2]));
  sum1bcc s3 (.A(xi[3]), .B(yi[3]), .Ci(c3), .Cout(co) ,.S(zi[3]));



endmodule
```

Para la simulación, generamos el TestBench 

```verilog
`timescale 1ns / 1ps
module sum4b_TB;

  reg [3:0] A;
  reg [3:0] B;

  wire co;
  wire [3:0] S;

  sum4b uut (
    .xi(A), 
    .yi(B), 
    .co(co), 
    .zi(S)
  );

  
  initial begin
  
    A=0;
	 for (B = 0; B < 16; B = B + 1) begin
      if (B==0)
        A=A+1;
      #5 ;
		$display("El valor de %d + %d = %d",A, B,S) ;
    end
	
  end      

  initial begin: TEST_CASE
     $dumpfile("sum4b_TB.vcd");
     $dumpvars(-1, uut);
     #(1200) $finish;
   end


endmodule
```
### 3. implementacion 

En mi caso no tengo la placa, así que los pasos siguientes fueron realizados junto con mis compañeros de grupo que si tiene las tarjetas físicas. 

se asigna la targe a utilizar, luego se asignan los pines que se utilizaran para sintetizar el programa 

Luego se visualizan las conexiones entre los pines y las entradas lógicas

Por último se conecta la placa por medio del cable USB, instalando los certificados y driver.

![image](https://user-images.githubusercontent.com/38961990/130364397-374f5433-a640-4475-923f-0e0d9418de65.png)
