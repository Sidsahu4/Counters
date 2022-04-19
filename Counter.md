# Counters
UPDOWN Counter
module counter_ct(clk, count, reset, up);
input  clk; 
input  reset;
input up;
 output [3:0]count;

 reg[3:0] count=0;
  

always@(posedge clk)
  begin
    if(reset==1)
  count<=0;
  else
  if(up)
    begin
      if(count==15)
        count<=0;
      else
        count++;
    end
  if(!up)
     begin
       if(count==0)
        count<=15;
      else
        count--;
    end
  end
endmodule
    
      



// or browse Examples
module counter_test();
  reg clk,reset,up;
  wire reg[3:0] count;
  
  //Instantiation
  counter_ct dut(clk,count,reset,up);
  
  initial
    begin
    clk=1'b0;
    forever #10 clk=~clk;
  end
  
  initial 
    begin
     reset=0; up=1;
    #50   reset=0; up=1;
    #50   reset=1; up=0;
    #50   reset=0; up=1;
    #50 $finish;
  end
  
  initial
    begin
      $monitor("At time=%t, clk=%b,count=%d, reset=%b, up=%b",$time,clk,count, reset, up);
      $dumpfile("counter.vcd");
      $dumpvars(0,counter_test);
    #500 $finish;
  end
endmodule


 
