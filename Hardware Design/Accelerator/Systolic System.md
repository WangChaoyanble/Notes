# Systolic System

**PE module :**

Receive `left` and `up` signal, first multiply and add to `sum`, then pass them to `right` and `down` for the right and down side PE.
```verilog
`define WIDTH_RES 8
`define WIDTH_NUM 4

module pe(  input clk,
            input rst,
            input [`WIDTH_NUM-1:0] left,
            input [`WIDTH_NUM-1:0] up,
            output reg [`WIDTH_NUM-1:0] down,
            output reg [`WIDTH_NUM-1:0] right,
            output reg [`WIDTH_RES-1:0] sum
            );

always@(posedge clk)begin
    if(rst) begin
        right<=0;
        down<=0;
        sum<=0;
        end
    else begin
        down<=up;
        right<=left;
        sum<=sum+left*up;
    end
end

endmodule
```

```verilog


```
