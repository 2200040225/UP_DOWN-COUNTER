# UP_DOWN-COUNTER

Design code:

module up_down_counter (
    input wire clk,         
    input wire reset,      
    input wire up_down,    
    output reg [7:0] count  
);

    always @(posedge clk or posedge reset) begin
        if (reset) 
            count <= 8'b0;  
        else if (up_down) 
            count <= count + 1;  
        else 
            count <= count - 1; 
    end

endmodule

Test bench:


module up_down_counter_tb;
    reg clk;
    reg reset;
    reg up_down;
    wire [7:0] count;
    up_down_counter uut (
        .clk(clk),
        .reset(reset),
        .up_down(up_down),
        .count(count)
    );
    always #5 clk = ~clk; 
    initial begin
        clk = 0;
        reset = 0;
        up_down = 0;
        reset = 1;
        #10;
        reset = 0;
        up_down = 1; 
        #100;      
        up_down = 0; 
        #100;  
        reset = 1;
        #10;
        reset = 0;
        up_down = 1; 
        #50;
        $finish;
    end
    initial begin
        $monitor("Time=%0t | Reset=%b | Up_Down=%b | Count=%d", $time, reset, up_down, count);
    end

endmodule

