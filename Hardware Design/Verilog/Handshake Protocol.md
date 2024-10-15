

```verilog
module send(
    input clk,
    input rst_n,
    output [7:0] reg data_out,

    output reg valid,
    input ready
);
reg [7:0] data_reg;
reg processed;
integer data_count=0;

always @(posedge clk or negedge rst_n) begin
    if(rst_n) begin
        data_out<=0;
        valid<=0;
        data_reg<=0;
        data_valid<=0;
        data_count<=0;
    end

    else begin
        //data is valid and receiver is ready to receive
        // set data out and valid
        if(processed && ready) begin
            data_out<=data_reg;
            valid<=1'b1;
            processed<=0;
            data_count<=data_count+1;
        end
        //if data is not valid
        if(~processed) begin
            data_reg<=data_count;
            processed<=1'b1;
            
        end

    end
end
endmodule

module receiver(
    input clk,
    input rst_n,
    input [7:0] data_in;

    output reg ready,
    input valid
);

reg[7:0] data[127:0];
reg processed;
integer i=0;
always @(posedge clk or negedge rst_n) begin
    if(rst_n) begin
        ready<=0;
        data_out<=0;
        processed<=0;
        for (integer i=0;i<127;i=i+1) begin
            data[i]<=0;
        end
    end
    else begin    //processed and sending data is valid
        if(valid && processed) begin
            data[i]<=data_in; //receive data
                
            processed<=0;   //not processed
        end

        if(~processed) begin
            i<=i+1;
            ready<=1'b1;
            process<=1'b1;
        end

    end
end

endmodule

```