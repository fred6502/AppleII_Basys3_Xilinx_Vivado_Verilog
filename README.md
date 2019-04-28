# AppleII_Basys3_Xilinx_Vivado_Verilog
This is a gate level more or less implementation of an Apple ][. It outputs a composite video signal and uses USB/PS2 keyboard. This is the Xilinx Vivado Project written in Verilog including a built Apple Vivado\AppleII\AppleIIGL2\AppleIIGL2.runs\impl_1\AppleII_FPGA.bit ready to be downloaded into basys3. Needs some external components to make composite video signal.

All the output pins are for debugging except four are used for the composite video signal and the speaker. 
Vivado\AppleII\AppleIIGL2\AppleIIGL2.srcs\sources_1\imports\sources_1\imports\AIIGateSch\AppleII_FPGA.v shows which output ports have the composite video: sync, data, colorburst as well as speaker. The AppleII schematic shows hot to use some resistors and a transistor to generate the voltage for the composite video signal.

Need to add support for VGA port. Timing is probably okay to buffer one video line to repeat it twice and do 640x400 or 640x480. Apple pixels (text, lo-res, or hi-res) are 280-horizontal x 192-vertical.. What about HDMI? it would be good to learn that protocol.

The top button toward USB connector is full hardware reset and the bottom one toward switches is softer reset like when you hit reset on the Apple II or maybe it's the other way around. AppleII_FPGA.v is where you look up what the swithces and buttons do. Switches can be used to see different debug info if you have a logic analyzer. The 3 video out signals + speaker are not affected by any switches.

It works... But certainly beta. I've been booting up. After reset you are in F800-FFFF monitor. To get to basic do CTRL-C or CTRL-B. I think CTRL-B erases your basic program. Last runs I was using Floating Point basic but it also has integer. That is selected by one of the switches. I should of made sure integer rom select still worked I haven't tested it since last got it all working again build.

Composite can be used with black and white or color composit monitor. Black and white is a-lot less picky about correct voices. Using some adjustable pots for each of the 3 signal voltages and an oscilloscope might be good to tune it good for color. Color timing is correct.. no color drift. 

Xilinx-ISE version had lots of color drift because couldn't select close enough to 14.31818 MHz clock. Composite video people will surely recognize that frequency.

Anyway have fun and remember nothing is coming out of the VGA port! external components for composite signal voltages. Recommend at first watch video signals with logic analyzer.. Watching address/data with logic analyzer is a great way to see its running. First thing 6502 does is read address at FFFC.FFFD and hop over there and party!
