Automated Screen Alignment for High-Speed Textile Oval Machines
The Mission
In textile printing, a misaligned screen is the difference between a premium t-shirt and a cleaning rag. Manually adjusting screens on a massive oval machine is a "neck-pain-inducing" task that kills productivity.

This project gives the Oval Machine a set of high-tech eyes. We’ve automated the 3-axis screen adjustment process, ensuring that every layer of ink hits the fabric with surgical precision—automatically.

The "Dream Team" (Architecture)
👁️ The Scout (Master RPi 5): Perched above the screen with a Camera Module 3. It uses OpenCV to hunt for registration marks (the "+" marks). It calculates the "misalignment math" in real-time.

📡 The Messenger (Slave RPi 5): Receives coordinate data via Wi-Fi. It acts as the bilingual diplomat, translating Python logic into Modbus commands that industrial hardware can understand.

🏗️ The Heavy Lifter (Delta AS228T PLC): The industrial backbone. It takes the "orders" and drives a 3-axis single stepper driver to physically shift the screen into the sweet spot.

Why This is a Game Changer for Textiles
Stop the "Stop-and-Go": Drastically reduces setup time between different print jobs.

Wireless Flexibility: Since the Master and Slave talk via Wi-Fi, we don’t have to run long, messy communication cables along the length of the oval track.

Micron Precision: Stepper motors don't get tired or make "human errors." If it's 0.2mm off, the PLC fixes it before the first squeegee stroke.

The Workflow (The "Ink-Sync")
Detect: Master RPi spots the registration mark on the screen.

Calculate: Python script determines the X, Y, and Rotation (Theta) error.

Beam: Data is shot across the shop floor via UDP Sockets.

Inject: Slave RPi injects these values directly into the Delta PLC registers.

Align: The PLC executes a coordinated 3-axis move. Result: Perfect Registration.

🛠 Tech Stack
Vision: OpenCV, Python (Master/Slave).

Industrial: Delta AS228T, Modbus TCP, ISPSoft (Ladder/Structured Text).

Motion: 3-Axis Stepper System.

💡 Fun Fact from the Factory Floor
"Before this system, aligning a 12-color job felt like a cardio workout. Now, I spend more time drinking chai while the Raspberry Pis do the squinting for me."
