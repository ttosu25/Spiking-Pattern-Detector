<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## Spiking Pattern Detector

![Architecture of LIF neuromorphic core](Spiking_Core_Schema.drawio.png)

Spiking Pattern Detector is an application of a neuromorphic processing core, implementing a 4-neuron Spiking architecture with fixed-point precision (Q8.8). The system generates an event when the temporal spike response of an input signal matches a user-defined pattern.

The core employs a discretised Leaky Integrate-and-Fire Model with a one-to-one neuron–synapse mapping. Synaptic weights are static, and the design operates without online learning (e.g. STDP).

This architecture serves as a foundation for exploring event-driven computation systems, including:

- Real-time signal processing (event-based DSP / sparse filtering)
- Temporal pattern recognition in spike-based data streams
- **Robotic sensing and reflex systems** (low-latency event detection)

## How to test

1. Input a pattern to be matched using input switches. LEDs on the board will light up in correspondance with the pattern.
2. Connect the IRF520 MOSFET Driver Module's signal port to output port 5 and wire it's power ports accordingly.
3. Connect a 3-6V motor between an external 3-6V battery and the MOSFET driver module.
4. Press n_reset on the microcontroller.
5. Input a symmetric 0.5Hz square-wave signal using a signal generator into input port 5, making sure to latch your signal to high or low for your first bit before you press n_reset. 

 - A green LED will flash each time the input is being sampled
 - The current spike pattern will be indicated by a separate set of red LEDs

 6. When the current spike pattern matches the pattern input by the user, the motor should rotate for a duration before returning to rest.

For demonstration purposes, the clock frequency has been deliberately set low (2 Hz) to make internal processing observable and to provide insight into system behaviour (e.g. a robotic reflex response).

Due to the state-dependent dynamics of the neurons, the spike response depends on both historical membrane state and current input values. You can experiment with different signals encoded using On-Off Keying (OOK), where logic ‘1’ corresponds to a high input level and ‘0’ to a low level, to observe how input sequences affect spike responses. Higher clock frequencies enable more responsive system behaviour.

## External hardware
- IRF520 MOSFET Driver Module
- 3-6V battery
- 3-6V (hobby) motor
