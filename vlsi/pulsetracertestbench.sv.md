module PulseTracer (
    input wire clk,
    input wire rst,
    input wire noisy_in,
    output reg pulse_out
);
    reg prev_in;

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            prev_in <= 0;
            pulse_out <= 0;
        end else begin
            prev_in <= noisy_in;
            pulse_out <= (~prev_in & noisy_in); // rising edge detector
        end
    end
endmodule
