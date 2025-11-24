# VSD-RISC-V-SoC-Tapeout-Program-Week-9
# 🌟 **Final Documentation & Reflection (VSDBabySoC Tapeout Journey)**

**“My Complete SoC Design Story from RTL → GDS → Post-Layout STA”**
📄 Based on Week 9 Task File 

---

# 🧭 **Introduction — My Journey Entering Week 9**

Week 9 is not just submission week — it feels like the *culmination* of everything I’ve learned, broken, fixed, debugged, and re-designed over almost two months.
I started with **zero understanding of physical design** and slowly built my SoC step-by-step:

* Learning how RTL becomes gates
* How gates become cells
* How cells become layout
* And how layout becomes timing-clean silicon

In Week 9, my job is to **assemble all my work into one GitHub repository** and reflect on my SoC-building experience in a clean, reproducible way.

This README is exactly that.
My full VSDBabySoC journey — documented from technical, conceptual, and personal angles.

---

# 🚀 **1. My Goal for Week 9**

To create a fresh, original GitHub repository that includes:

✔ Complete week-wise documentation
✔ My commands, screenshots, logs
✔ My SoC experiments & modifications
✔ My understanding of SPEF, STA, routing, timing closure
✔ A truthful engineering journey

This README acts as the front page of that submission.

---

# 🏗️ **2. My VSDBabySoC Tapeout Journey — Week Wise Breakdown**

Below is my **hands-on timeline** of how I built a minimal SoC from scratch.

---

# 🧩 **Week 1 — Understanding the SoC Universe**

This week was my warmup.

### What I learned:

* What is an SoC? (Processor + memories + peripherals + interconnects)
* What is SKY130?
* What is OpenLane?
* How the “RTL → GDS” journey works

### Commands I ran:

```bash
sudo apt-get install yosys magic iverilog gtkwave
git clone https://github.com/The-OpenROAD-Project/OpenLane
```

### What confused me:

* Why do we need so many files? (.lib, .lef, .gds, .spef?)
* What is a PDK exactly?

### Special Note

> The PDK is like the rulebook for silicon. Without the rules, the chip is illegal.

---

# 🛠️ **Week 2 — RTL & Synthesis (My First Step into Hardware Reality)**

### Tasks I did:

* Wrote/understood the VSDBabySoC RTL
* Ran synthesis with Yosys

### Commands:

```bash
yosys -s synth.tcl
```

### What I learned:

* RTL is NOT hardware — synthesis makes hardware
* Timing constraints (SDC) are the “rules” for synthesis
* Setup time & hold time first appear here

### Why Synthesis matters:

Because without synthesis, your SoC is just text — not hardware.

---

# 🧮 **Week 3 — My First STA (Static Timing Analysis)**

This week was the **moment I understood timing**.

### Commands:

```tcl
read_liberty sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog synth.v
read_sdc constraints.sdc
report_checks -path_delay max
```

### What I learned:

* Arrival time vs required time
* WNS (Worst Negative Slack)
* Why SS corner fails setup
* Why FF corner fails hold

### Special Note

> Timing is the soul of a chip. A chip with bad timing = a chip that doesn’t boot.

---

# 🏗️ **Week 4 — Floorplanning (Giving Shape to My Chip)**

This week felt like designing the “home” for all my cells.

### Commands:

```bash
run_floorplan
```

### I learned:

* Die area
* Core area
* Pin placement
* Macro orientation

### My doubt:

Why is utilization important?
→ Because too much density = congestion = routing failure.

---

# 🧱 **Week 5 — Placement (Organizing Millions of Lego Blocks)**

This was surprisingly fun.

### Commands:

```bash
run_placement
```

### What I learned:

* Global vs detailed placement
* Legalization
* Standard cell alignment
* Congestion maps

### Realization:

> Placement determines 50% of timing success.
> If placement is bad → routing will suffer → timing will break → silicon will fail.

---

# ⏰ **Week 6 — Clock Tree Synthesis (Making Time Flow Inside SoC)**

Clock is the heartbeat of the chip.

### Commands:

```bash
run_cts
```

### I learned:

* Skew
* Latency
* Clock buffers
* H-tree structure

### Why CTS broke my timing:

Because inserting clock buffers changes delays → new setup/hold behaviors.

---

# 🧭 **Week 7 — Routing (The Hardest Week for Me)**

### Commands:

```bash
run_routing
```

### What I learned:

* Global routing
* Detailed routing
* DRC checks
* Why vias are expensive
* Why spacing matters

### Big lesson:

> You don’t route your chip.
> The tools route it *based on how well YOU floorplanned and placed it.*

---

# 🔍 **Week 8 — SPEF & Multi-Corner STA (The Real Silicon Check)**

📄 Based on Week 8 Summary File (from previous conversation)

### Commands:

```tcl
read_spef routed.spef
report_checks -path_delay max
report_checks -path_delay min
```

### What I learned:

* SPEF contains R + C values of every routed net
* Post-route timing is the closest to real silicon timing
* Week-3 vs Week-8 comparison shows the effect of parasitics

### My observation:

* WNS became worse
* Hold slack changed
* Coupling capacitance affected critical paths

### Special Note

> Post-route STA decides if your SoC is **tapeout-ready**, not pre-route STA.

---

# 🎉 **Week 9 — Final Documentation & Submission (This Week)**

Week 9 is about presenting everything I did.

### Tasks:

* Organizing screenshots
* Writing detailed README
* Making step-by-step instructions
* Highlighting unique experiments
* Ensuring all terminal outputs have **my username visible**
* Creating a clean GitHub repo

### Why Week 9 is the most important:

Because documentation differentiates an engineer from someone who only runs commands.

---

# 🔥 **3. Unique Experiments I Performed**

These are the custom efforts I performed in my VSDBabySoC flow:

### ✔ Customizing config.tcl values

I changed:

* `FP_CORE_UTIL`
* `CLOCK_PERIOD`
* `PL_TARGET_DENSITY`

### ✔ Modified clock buffer selection in CTS

### ✔ Re-ran multi-corner STA manually

### ✔ Verified SPEF impact by comparing two routing attempts

### ✔ Added custom scripts for report extraction

---

# ❓ **4. Q&A — Real Questions I Asked Myself During SoC Building**

### **Q1: Why does timing break after routing even when it passed in synthesis?**

Because routing introduces **real wire RC parasitics**, which drastically increase delay.

---

### **Q2: Why does SS corner always show worst setup timing?**

Because slow transistors + low voltage = maximum delay = setup failures.

---

### **Q3: Why is FF corner worst for hold?**

Because fast devices + high voltage make signals arrive too early.

---

### **Q4: Why do we need SPEF when .lib already contains delays?**

.lib contains **cell delays**
SPEF contains **wire delays**
Real timing = cell delay + wire delay

---

### **Q5: Why is documentation mandatory for tapeout training?**

Because tapeout is teamwork — and a team is only as strong as its documentation.

---

# 📌 **Special Notes & SoC Facts**

### ⭐ Fact 1

> 70% of delay in modern nodes is from routing, not gates.
> That is why SPEF-based STA matters.

### ⭐ Fact 2

> A chip with +0.001 ns slack works.
> A chip with –0.001 ns slack fails.

### ⭐ Fact 3

> CTS changes timing more than placement or routing.

### ⭐ Fact 4

> Final GDS is not just a pretty image —
> It is EXACTLY what goes to silicon.

### ⭐ Fact 5

> Good documentation = professional engineer.
> No documentation = disqualified candidate.

---

# 🏁 **5. Conclusion — My Final Thoughts**

Completing VSDBabySoC was a **transformative engineering experience** for me.

I entered this program thinking silicon design was too complex.
I am leaving this program knowing that:

* I can run a complete RTL-to-GDS flow
* I can analyze timing across PVT corners
* I can debug synthesis, placement, CTS, and routing
* I can work like a real SoC physical design engineer

Week 9 feels like the graduation ceremony of my tapeout journey.


