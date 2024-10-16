

```verilog
module send(
    input clk,
    input rst_n,

    input ready,
    output reg valid,

    output reg [7:0] data
);
reg [7:0]data_reg;
integer i=0;
always @(posedge clk or negedge rst_n) begin

    if(!rst_n) begin
        valid<=0;
        data_reg<=0;
        data<=0;
    end
    else begin
        if(valid && ready) begin 
        //data is sending, first set valid 0, then we can do other things
        //remember we need to keep the out data stable, so don't do andy thing to it
            valid<=0;
            i<=i+1;
        end
        if(!valid) begin   
            //preparing data and set valid 1
            data<=i;
            valid<=1'b1;
        end
    end
end
endmodule

module receive(
    input clk,
    input rst_n,

    input valid,
    input [7:0] data,
    output reg ready
);
reg [7:0] data_reg[127:0];
integer j=0;
always @(posedge clk or negedge rst_n) begin
    if(!rst_n) begin
        ready<=0;
        for(integer i=0;i<128;i=i+1) begin
            data_reg[i]<=0;
        end
    end
    else begin
        if(valid && ready) begin //storing data, set ready 0
            data_reg[j]<=data;
            ready<=0;
        end
        if(!ready) begin  //preparing to receiving data(like storage for the data), then set ready 1
            j<=j+1;
            ready<=1;
        end
    end

end


endmodule

`timescale 1ns / 1ps

module test(

    );
    wire valid;
    wire ready;
    wire [7:0] data;
    reg clk;
    reg reset;
    send moduleA (.clk(clk),.data(data),.rst_n(reset),.ready(ready),.valid(valid));
    receive moduleB (.clk(clk),.data(data),.rst_n(reset),.ready(ready),.valid(valid));
    initial begin
        clk = 0;
        forever #5 clk = ~clk; // 10ns周期
    end

    // 复位序列
    initial begin
        reset = 0;
        #10;
        reset = 1;
        #200;
        
    end
endmodule


```