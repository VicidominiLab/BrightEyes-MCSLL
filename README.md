# BrightEyes-MCSLL
The BrightEyes Microscope Control Software Low-Level is a collections of firmwares for NI FPGA in order to be used with BrightEyes-MCS.
Documentation and usage you can find in [BrightEyes-MCS repository](https://github.com/VicidominiLab/BrightEyes-MCS).


**Copyright** (C) 2023 Istituto Italiano di Tecnologia

**Author:** Mattia Donato

**Credits to:** Marco Castello, Giorgio Tortarolo, Simonluca Piazza, Eli Slenders

**Closed-Source Firmware License Agreement:** This license grants you a non-exclusive, non-transferable permission to download and utilize our proprietary firmware free of charge. However, you are required to use this firmware exclusively in conjunction with open-source software, such as [BrightEyes-MCS](https://github.com/VicidominiLab/BrightEyes-MCS). Modifying, distributing, or employing it with closed-source software is strictly prohibited. We actively endorse and support the use of this firmware in educational institutions, including schools, universities, as well as in both public and private research organizations. All rights to the firmware are retained by us. The firmware is provided "as is" with absolutely no warranty. We disclaim all liability for any damages. This license may be terminated at your discretion or by us. Your use of the firmware signifies your agreement to this Agreement.

If you have bugs to report or you have requests for adding or modifying firmware functionalities, please feel free to contact us. We are open to collaborations!

## Available firmware

| Firmware path | NI board | I/O | Notes | DFD mode |
|---------------|----------|-----|-------|----------|
| `MCSv2-PCIe7820R-3_3V-40M91.lvbitx` | NI PCIe-7820R | 3.3 V | Standard firmware | Laser exc. 40 MHz/91 bins |
| `MCSv2-PXIe7822R-3_3V-40M91.lvbitx` | NI PXIe-7822R | 3.3 V | Standard firmware | Laser exc. 40 MHz/91 bins |
| `MCSv2-PXIe7856R-3_3V-40M91.lvbitx` | NI PXIe-7856R | 3.3 V | Standard firmware | Laser exc. 40 MHz/91 bins |
| `MCSv2-USB7856R-3_3V-40M91.lvbitx` | NI USB-7856R | 3.3 V | Standard firmware | Laser exc. 40 MHz/91 bins |

## Contents

- **FPGA interface**
  - [Registers](#registers)
  - [FIFO streams](#fifo-streams)
- **Reference**
  - [Version history](#version-history)
  - [Pinout overview](#pinout-overview)
  - [Detector bit allocation](#detector-bit-allocation)
  - [Channel numbering](#channel-numbering)
  - [DFD frequency](#dfd-frequency)

## Registers

| Name                           | Type       | Read/Write | Description                                                                                                                                      |
|--------------------------------|------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| **Main**                       |            |            |                                                                                                                                                  |
| start_command                  | Bool       | RW         | Start the scanning                                                                                                                               |
| stop_command                   | Bool       | RW         | Stop the scanning                                                                                                                                |
| debug_scan_fsm_status          | I16        | R          | Status of the FSM                                                                                                                                |
|                                |            |            |                                                                                                                                                  |
| **Scan Settings**              |            |            |                                                                                                                                                  |
| time_bin_dwell_cycles          | I32        | RW         | Wait cycles per bin in 40 MHz clock units (default: 40)                                                                                          |
| max_time_bins_per_pixel        | I32        | RW         | Number of time bins per pixel                                                                                                                    |
| max_pixel                      | I32        | RW         | Number of pixels (X)                                                                                                                             |
| max_line                       | I32        | RW         | Number of lines (Y)                                                                                                                              |
| max_frame                      | I32        | RW         | Number of frames (Z)                                                                                                                             |
| max_repetition                 | I32        | RW         | Number of repetitions (REP)                                                                                                                      |
| axis_start_offset_volts        | Fxp-Array  | RW         | Array [x,y,z] offset in V                                                                                                                        |
| axis_calibration_volts_per_step | Fxp-Array | RW         | Array [x,y,z] calibration in V/step                                                                                                              |
| xy_snake_scan_enable           | Bool       | RW         | If enabled the scanning is performed as "snake-scanning" else use the normal "raster scanning" (default: False)                                  |
| z_snake_scan_enable            | Bool       | RW         | Enable snake scanning along the Z axis                                                                                                            |
|                                |            |            |                                                                                                                                                  |
| **Analog Output**              |            |            |                                                                                                                                                  |
| N = 0, ..., 7                  |            |            | Replace `N` with the analog output channel number                                                                                                |
| analog_output_N_volts          | Fxp        | R          | Current voltage on analog output N                                                                                                                |
| analog_output_N_source_selector | U8        | RW         | Source for analog output N: 0 = X, 1 = Y, 2 = Z, otherwise use the constant DC value                                                            |
| analog_output_N_dc_volts       | Fxp        | RW         | Constant DC voltage for analog output N                                                                                                           |
|                                |            |            |                                                                                                                                                  |
| **Scanning Status**            |            |            |                                                                                                                                                  |
| current_line_parity_flag       | Bool       | R          | Current line parity (for snake scanning)                                                                                                         |
| current_cycle_index            | I32        | R          | Current cycle                                                                                                                                    |
| current_time_bin_index         | I32        | R          | Current time bin                                                                                                                                 |
| current_x_index                | I32        | R          | Current X index                                                                                                                                  |
| current_y_index                | I32        | R          | Current Y index                                                                                                                                  |
| current_z_index                | I32        | R          | Current Z index                                                                                                                                  |
| current_repetition_index       | I32        | R          | Current repetition                                                                                                                               |
| current_circular_point_index   | I32        | R          | Current circular-scan point index                                                                                                                 |
| current_circular_repetition_index | I32     | R          | Current circular-scan repetition index                                                                                                            |
| current_laser_time_bin_index   | U8         | R          | Current laser time-bin index                                                                                                                      |
|                                |            |            |                                                                                                                                                  |
| **Detection Configuration**    |            |            |                                                                                                                                                  |
| wait_initialization_time_in_us | U32        | RW         | SPAD configuration - time to wait before starting acquisition, in microseconds                                                                   |
| spad_configuration_message     | U64        | RW         | SPAD configuration command message                                                                                                               |
| spad_configuration_message_length | U8      | RW         | SPAD configuration message length                                                                                                                |
| spad_sdata_invert_enable       | Bool       | RW         | Invert the SPAD configuration command logic (useful for some SPAD prototypes)                                                                     |
| tag_clock_duration_cycles      | I64        | RW         | SPAD configuration sync output duration, in 40 MHz clock cycles                                                                                  |
| detector_fpga_holdoff_cycles   | U16        | RW         | FPGA-based detector holdoff time, in 120 MHz clock cycles                                                                                        |
| dummy_data_enable              | Bool       | RW         | Produce dummy data instead of using data from the detector                                                                                       |
| detector_49_channel_mode_enable | Bool      | RW         | Enable 49-channel detector mode                                                                                                                   |
| spad_vr0_enable                | Bool       | RW         | Enable the SPAD VR0 configuration signal                                                                                                          |
| spad_vr1_enable                | Bool       | RW         | Enable the SPAD VR1 configuration signal                                                                                                          |
|                                |            |            |                                                                                                                                                  |
| **Laser Control**              |            |            |                                                                                                                                                  |
| wait_laser_startup_cycles      | I64        | RW         | Wait after turning on the laser, in 40 MHz clock cycles                                                                                          |
| wait_post_frame_cycles         | I64        | RW         | Wait after frame completion, in 40 MHz clock cycles                                                                                              |
| wait_laser_first_time_only_enable | Bool    | RW         | Wait after turning on the laser only the first time                                                                                              |
| laser_off_after_measurement_enable | Bool   | RW         | Turn off the laser after a measurement                                                                                                           |
| laser_excitation_sequence      | U8-Array   | RW         | Array[24] laser excitation sequence; the used portion runs from index 0 to the value of `firmware_dfd_fast_to_excitation_frequency_ratio`       |
| laser_force_pulsing_enable     | Bool       | RW         | Force laser pulsing                                                                                                                               |
| laser_time_bin_mode_enable     | Bool       | RW         | Enable laser time-bin mode                                                                                                                        |
| max_laser_time_bin             | U8         | RW         | Maximum laser time-bin index                                                                                                                      |
|                                |            |            |                                                                                                                                                  |
| **Circular Scanning Settings** |            |            |                                                                                                                                                  |
| circular_scan_x_volts          | Fxp-Array  | RW         | Array[32] of X voltages for circular scanning                                                                                                        |
| circular_scan_y_volts          | Fxp-Array  | RW         | Array[32] of Y voltages for circular scanning                                                                                                        |
| circular_scan_z_volts          | Fxp-Array  | RW         | Array[32] of Z voltages for circular scanning                                                                                                        |
| circular_scan_enable           | Bool       | RW         | Use circular scanning with `circular_scan_x_volts` or data supplied through `stream_in`                                                          |
| max_circular_point             | I32        | RW         | Maximum circular-scan point index                                                                                                                 |
| max_circular_repetition        | I32        | RW         | Maximum number of circular-scan repetitions                                                                                                       |
|                                |            |            |                                                                                                                                                  |
| **Scanning LImits**            |            |            |                                                                                                                                                  |
| max_x_volts                    | Fxp        | RW         | Maximum X voltage                                                                                                                                |
| max_y_volts                    | Fxp        | RW         | Maximum Y voltage                                                                                                                                |
| max_z_volts                    | Fxp        | RW         | Maximum Z voltage                                                                                                                                |
| min_x_volts                    | Fxp        | RW         | Minimum X voltage                                                                                                                                |
| min_y_volts                    | Fxp        | RW         | Minimum Y voltage                                                                                                                                |
| min_z_volts                    | Fxp        | RW         | Minimum Z voltage                                                                                                                                |
|                                |            |            |                                                                                                                                                  |
| **FIFO Settings**              |            |            |                                                                                                                                                  |
| stream_out_aux_enable          | Bool       | RW         | Enable the auxiliary output stream                                                                                                               |
| stream_out_main_enable         | Bool       | RW         | Enable the main output stream                                                                                                                    |
| internal_fifo_analog_overflow_flag | Bool   | R          | True when the internal analog FIFO has overflowed at least once during the scan                                                                  |
| internal_fifo_spad_overflow_flag | Bool     | R          | True when the internal SPAD FIFO has overflowed at least once during the scan                                                                    |
| stream_out_aux_overflow_cycle_counter | U64 | R         | Number of cycles in which the auxiliary output stream overflowed during the scan                                                                |
| stream_out_main_overflow_cycle_counter | U64 | R        | Number of cycles in which the main output stream overflowed during the scan                                                                      |
| redirect_intensity_to_stream_out_aux_enable | Bool | RW  | Redirect intensity data to the auxiliary output stream                                                                                           |
|                                |            |            |                                                                                                                                                  |
| **Laser Enable**               |            |            |                                                                                                                                                  |
| laser_1_enable                 | Bool       | RW         | Enable laser 1                                                                                                                                   |
| laser_2_enable                 | Bool       | RW         | Enable laser 2                                                                                                                                   |
| laser_3_enable                 | Bool       | RW         | Enable laser 3                                                                                                                                   |
| laser_4_enable                 | Bool       | RW         | Enable laser 4                                                                                                                                   |
|                                |            |            |                                                                                                                                                  |
| **Analog Input**               |            |            |                                                                                                                                                  |
| analog_a_input_selector        | U8         | RW         | Select the analog input for analog channel A                                                                                                     |
| analog_b_input_selector        | U8         | RW         | Select the analog input for analog channel B                                                                                                     |
|                                |            |            |                                                                                                                                                  |
| analog_a_differential_mode_enable | Bool    | RW         | True: signal derivative within the time bin; False: direct signal                                                                                |
| analog_b_differential_mode_enable | Bool    | RW         | True: signal derivative within the time bin; False: direct signal                                                                                |
|                                |            |            |                                                                                                                                                  |
| N = 0, ..., 7                  |            |            | Replace `N` with the analog input channel number                                                                                                 |
| analog_a_channel_N_invert_enable | Bool     | RW         | Invert analog A channel N                                                                                                                         |
| analog_a_channel_N_integrate_enable | Bool  | RW         | Integrate analog A channel N at the maximum ADC readout speed                                                                                     |
| analog_input_N_volts           | Fxp        | R          | Current voltage on analog input N                                                                                                                 |
|                                |            |            |                                                                                                                                                  |
| **Digital Frequency Domain**   |            |            |                                                                                                                                                  |
| L1                             | U8         | RW         | A state of laser sync for DFD - AAA_AAA_BBB_BBB                                                                                                  |
| L2                             | U8         | RW         | B state of laser sync for DFD - AAA_000_BBB_000                                                                                                  |
| L3                             | U8         | RW         | C state of laser sync for DFD - AA0_0BB_00C_C00                                                                                                  |
| L4                             | U8         | RW         | D state of laser sync for DFD - A00_B00_C00_D00                                                                                                  |
| dfd_enable                     | Bool       | RW         | Enable DFD                                                                                                                                       |
| dfd_dwell_time_cycles_120mhz   | U32        | RW         | Interval for transmitting a full histogram, in 120 MHz clock cycles (default: 1e6; usually not used)                                             |
| dfd_internal_dwell_time_enable | Bool       | RW         | False: use pixel-index parity to trigger DFD histogram transmission; True: use the configured dwell time (default: False)                        |
| dfd_laser_sync_debug_enable    | Bool       | RW         | True: channel 26 becomes the laser time reference for phasor analysis; False: channel 26 is connected to extra channel 1                         |
| dfd_current_position_index     | Fxp        | R          | Current DFD position index                                                                                                                       |
| dfd_transmitted_position_index | Fxp        | R          | Transmitted DFD position index                                                                                                                   |
| dfd_acquisition_active_status  | Bool       | R          | Whether DFD acquisition is active                                                                                                                |
| internal_fifo_dfd_overflow_flag | Bool      | R          | Status of the internal DFD FIFO overflow                                                                                                         |
| dfd_bin_count                  | U16        | R          | Number of DFD bins                                                                                                                                |
| dfd_trigger_selector           | I8         | RW         | Select the DFD trigger source                                                                                                                     |
| firmware_dfd_fast_to_excitation_frequency_ratio | U8 | R | Firmware DFD fast-clock to excitation-frequency ratio                                                                                            |
|                                |            |            |                                                                                                                                                  |
| **Firmware Configuration / Status** |       |            |                                                                                                                                                  |
| firmware_external_clock_active_flag | Bool  | R          | External firmware clock is active                                                                                                                 |
| firmware_external_dac_active_flag | Bool    | R          | External DAC support is active                                                                                                                    |
| firmware_force_25_channel_mode_active_flag | Bool | R    | Forced 25-channel detector mode is active                                                                                                         |
| firmware_gi_dac_adc_active_flag | Bool      | R          | GI DAC/ADC support is active                                                                                                                      |
| gi_dac_adc_short_cable_mode_enable | Bool   | RW         | Enable GI DAC/ADC short-cable mode                                                                                                                |
|                                |            |            |                                                                                                                                                  |
| **Slave Mode**                 |            |            |                                                                                                                                                  |
| slave_mode_enable              | Bool       | RW         | Enable slave mode                                                                                                                                |
| slave_mode_emulated_pixel_count | Bool      | R          | Indicates that the slave-mode pixel count is emulated                                                                                            |
| slave_mode_event_count         | U32        | R          | Current slave-mode event count                                                                                                                    |
| slave_mode_external_source_selector | U8    | RW         | Select the external slave-mode event source                                                                                                       |
| slave_mode_max_event_count     | U32        | RW         | Maximum slave-mode event count                                                                                                                    |
| slave_mode_test_generator_enable | Bool     | RW         | Enable the slave-mode test generator                                                                                                              |
|                                |            |            |                                                                                                                                                  |
| **Custom Scanning Position**   |            |            |                                                                                                                                                  |
| custom_positions_enable        | Bool       | RW         | Enable custom scanning positions supplied through `stream_in`                                                                                    |
| custom_positions_last_pixelwise_address | U32 | R       | Internal use / Debug                                                                                                                             |
| custom_positions_last_framewise_address | U32 | R       | Internal use / Debug                                                                                                                             |
| custom_positions_stream_in_ready_flag | Bool | R        | Internal use / Debug                                                                                                                             |
| custom_positions_current_address | U32     | R          | Internal use / Debug                                                                                                                             |
| custom_positions_x_volts      | Fxp        | R          | Internal use / Debug                                                                                                                             |
| custom_positions_y_volts      | Fxp        | R          | Internal use / Debug                                                                                                                             |
| custom_positions_z_volts      | Fxp        | R          | Internal use / Debug                                                                                                                             |
| custom_positions_tx_begin_flag | Bool      | R          | Internal use / Debug                                                                                                                             |
| custom_positions_extra_flag   | Bool       | R          | Internal use / Debug                                                                                                                             |
| custom_positions_update_mode_flag | Bool  | R          | Internal use / Debug                                                                                                                             |
| custom_positions_tx_end_flag  | Bool       | R          | Internal use / Debug                                                                                                                             |
| custom_positions_offset_current_address | U32 | R      | Internal use / Debug                                                                                                                             |
| custom_positions_offset_x_volts | Fxp      | R          | Internal use / Debug                                                                                                                             |
| custom_positions_offset_y_volts | Fxp      | R          | Internal use / Debug                                                                                                                             |
| custom_positions_offset_z_volts | Fxp      | R          | Internal use / Debug                                                                                                                             |
| custom_positions_offset_tx_begin_flag | Bool | R       | Internal use / Debug                                                                                                                             |
| custom_positions_offset_extra_flag | Bool | R          | Internal use / Debug                                                                                                                             |
| custom_positions_offset_update_mode_flag | Bool | R    | Internal use / Debug                                                                                                                             |
| custom_positions_offset_tx_end_flag | Bool | R         | Internal use / Debug                                                                                                                             |
|                                |            |            |                                                                                                                                                  |
| **Internal / Debug**           |            |            |                                                                                                                                                  |
| shutter_enable                 | Bool-Array | RW         | Internal use / Debug                                                                                                                             |
| debug_pixel_tag                | Bool       | RW         | Internal use / Debug                                                                                                                             |
| debug_line_tag                 | Bool       | RW         | Internal use / Debug                                                                                                                             |
| debug_frame_tag                | Bool       | RW         | Internal use / Debug                                                                                                                             |
| debug_repetition_tag           | Bool       | RW         | Internal use / Debug                                                                                                                             |
| debug_end_of_frame_flag        | Bool       | RW         | Internal use / Debug                                                                                                                             |
| debug_line_counter             | I64        | RW         | Internal use / Debug                                                                                                                             |
| tag_turnoff_pixel_counter      | I64        | R          | Internal use / Debug                                                                                                                             |
| tag_turnoff_line_counter       | I64        | R          | Internal use / Debug                                                                                                                             |
| tag_turnoff_frame_counter      | I64        | R          | Internal use / Debug                                                                                                                             |
| debug_t                        | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_x_index                  | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_y_index                  | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_z_index                  | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_x_index_2                | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_y_index_2                | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_z_index_2                | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_repetition_index         | I32        | RW         | Internal use / Debug                                                                                                                             |
| debug_circular_point_index     | I32        | RW         | Internal circular-scan point index                                                                                                                |
| debug_circular_repetition_index | I32       | RW         | Internal circular-scan repetition index                                                                                                           |
| debug_circular_repetition_tag  | Bool       | RW         | Internal circular-scan repetition tag                                                                                                             |

## FIFO streams

| Type | Name            | Data type | Read/Write                         | Purpose                                            |
|------|-----------------|-----------|------------------------------------|----------------------------------------------------|
| 1    | stream_in       | U64       | Write <br> \(from PC to FPGA\)     | Used only for the special case "custom positions"  |
| 2    | stream_out_main | U64       | Read <br> \(from FPGA to PC\)      | Data from SPAD acquired from digital channels 25+2 |
| 3    | stream_out_aux  | U64       | Read <br> \(from FPGA to PC\)      | Data from selected analog inputs A and B           |

### Data format:

- [Channels](#channels)
- [Main output stream (`stream_out_main`)](#main-output-stream-stream_out_main)
  - [25-channel format](#25-channel-format)
  - [49-channel format](#49-channel-format)
- [Auxiliary output stream (`stream_out_aux`)](#auxiliary-output-stream-stream_out_aux)

#### Channels
Channels position on SPAD array 5x5.

|    |    |     |    |    |
|----|----|-----|----|----|
| 0  | 1  | 2   | 3  | 4  |
| 5  | 6  | 7   | 8  | 9  |
| 10 | 11  | 12  | 13  | 14  |
| 15 | 16  | 17   | 18  | 19  |
| 20 | 21  | 22   | 23  | 24  |

Moreover there are two extra channels called 25 and 26.

#### Main output stream (`stream_out_main`)

Data from the SPAD detector is packed into consecutive unsigned 64-bit (`U64`) words. The number of words and the width of each channel field depend on the detector mode. In the layouts below, fields are listed from the least-significant bit (bit 0) to the most-significant bit (bit 63), and `channel[width]` denotes a channel followed by its field width in bits.

##### 25-channel format

Each acquisition sample consists of two consecutive `U64` words. The 25 detector channels have different field widths: central channels receive more bits than peripheral channels.

Field width for each detector channel:

|    |    |     |    |    |
|----|----|-----|----|----|
| 4  | 4  | 4   | 4  | 4  |
| 4  | 5  | 6   | 5  | 4  |
| 4  | 6  | 10  | 6  | 4  |
| 4  | 5  | 6   | 5  | 4  |
| 4  | 4  | 4   | 4  | 4  |

Channels 25 and 26 are auxiliary channels and use 5 bits each. Their fields occupy bits 0–4 of words 0 and 1, respectively.

| Word | Packed fields, from bit 0 to bit 63 |
|------|--------------------------------------|
| 0 | `25[5] → 0[4] → 1[4] → 2[4] → 3[4] → 4[4] → 5[4] → 17[6] → 18[5] → 19[4] → 20[4] → 21[4] → 22[4] → 23[4] → 24[4]` |
| 1 | `26[5] → 6[5] → 7[6] → 8[5] → 9[4] → 10[4] → 11[6] → 12[10] → 13[6] → 14[4] → 15[4] → 16[5]` |

##### 49-channel format

Each acquisition sample consists of eight consecutive `U64` words. Channels 0–48 are the 49 detector channels; channels 49 and 50 are auxiliary channels. The upper four bits of word 7 are unused.

| Word | Packed fields, from bit 0 to bit 63 |
|------|--------------------------------------|
| 0 | `16[16] → 17[16] → 18[16] → 23[16]` |
| 1 | `25[16] → 30[16] → 31[16] → 32[16]` |
| 2 | `24[16] → 2[8] → 3[8] → 4[8] → 8[8] → 9[8] → 11[8]` |
| 3 | `14[8] → 15[8] → 19[8] → 20[8] → 21[8] → 27[8] → 28[8] → 29[8]` |
| 4 | `33[8] → 34[8] → 36[8] → 37[8] → 39[8] → 40[8] → 44[8] → 45[8]` |
| 5 | `0[7] → 1[7] → 5[7] → 6[7] → 7[7] → 13[7] → 35[7] → 41[7] → 46[8]` |
| 6 | `10[14] → 22[14] → 42[7] → 43[7] → 47[7] → 48[7] → 12[8]` |
| 7 | `26[14] → 38[14] → 49[16] → 50[16] → unused[4]` |




#### Auxiliary output stream (`stream_out_aux`)
A word of U64 the first U32 bits are corresponding to the Analog A, and the other U32 bits are corresponding to the Analog B.

## Version history

| Date | Internal commit | Branch | Comments |
| --- | --- | --- | --- |
| 2025-11-24 | eb2c5574 | new_lut | Support the control of SPAD 7x7 pin VR0 and VR1 (for setting configuring the SPAD hold-off) |
|  |  |  | Internal: new clock frequency for the slave mode |
|  |  |  | Internal repository commit: |
|  |  |  | It should work with BrightEyes-MCS software commit >= b4e42d1 |
|  |  |  | ( https://github.com/VicidominiLab/BrightEyes-MCS/commit/b4e42d16fb76d905c75839f061c7a058f73863b9 ) |
| 2025-11-25 | 87bc7074 | new_lut | Changed internal notation and now VR0 and VR1 should work |
| 2025-11-27 | 0dff4934 | main | The DFD support the EXTERNAL CLOCK @40 MHz  (Should support a range 33.3 MHz up 52 MHz) |

## Pinout Overview

- [NI PCIe-7820R and NI PXIe-7822R](#ni-pcie-7820r-and-ni-pxie-7822r)
- [NI USB-7856R](#ni-usb-7856r)
- [NI PXIe-7856R](#ni-pxie-7856r)
- [GENOA INSTRUMENT — GI-BOX (PRISM)](#genoa-instrument--gi-box-prism)
- [GENOA INSTRUMENT — GI-DAC](#genoa-instrument--gi-dac)

### NI PCIe-7820R and NI PXIe-7822R

> Important: on the NI breakout board, DIO is not the pin number.

| NI Connector | DIO | Firmware Naming | GI-BOX |
| --- | --- | --- | --- |
| 0 | 0 | SPAD0 |  |
| 0 | ... |  |  |
| 0 | 24 | SPAD24 |  |
| 0 | 25 | SPAD_ENABLE | ENABLE |
| 0 | 26 | SPAD_VR0 | VR0 |
| 0 | 27 | SPAD_VR1 | VR1 |
| 0 | 28 | LASER_0 | AUX0 |
| 0 | 29 | LASER_1 | AUX1 |
| 0 | 30 | LASER_2 | AUX2 |
| 0 | 31 | LASER_3 | AUX3 |
|  |  |  |  |
| 1 | 0 | SPAD25 |  |
| 1 | ... |  |  |
| 1 | 23 | SPAD48 |  |
| 1 | 24 | SPAD_SDATA | SDA |
| 1 | 25 | SPAD_SCLK | SCL |
| 1 | 26 | DET_EXTRA_0 | AUX4 |
| 1 | 27 | DET_EXTRA_1 | AUX5 |
| 1 | 28 |  | AUX6 |
| 1 | 29 | PIXEL_SYNC | AUX7 |
| 1 | 30 | LINE_SYNC | AUX8 |
| 1 | 31 | FRAME_SYNC | AUX9 |
|  |  |  |  |
| 2 | 8 | AO_TRIGGER_TEST |  |
| 2 | 26 | AD5764_SDATA |  |
| 2 | 27 | AD5764_SCLK |  |
| 2 | 28 | AD5764_SSYNC |  |
|  |  |  |  |
| 3 | 0 | GI_DAC_SCLK0 |  |
| 3 | 1 | GI_DAC_SDIN0 |  |
| 3 | 2 | GI_DAC_SSYNC0 |  |
| 3 | 3 | GI_DAC_SCLK1 |  |
| 3 | 4 | GI_DAC_SDIN1 |  |
| 3 | 5 | GI_DAC_SSYNC1 |  |
| 3 | 6 | GI_DAC_SCLK2 |  |
| 3 | 7 | GI_DAC_SDIN2 |  |
| 3 | 8 | GI_DAC_SSYNC2 |  |
| 3 | 9 | GI_DAC_SCLK3 |  |
| 3 | 10 | GI_DAC_SDIN3 |  |
| 3 | 11 | GI_DAC_SSYNC3 |  |
| 3 | 12 | GI_DAC_SCLK4 |  |
| 3 | 13 | GI_DAC_SDIN4 |  |
| 3 | 14 | GI_DAC_SSYNC4 |  |
| 3 | 15 | GI_DAC_GI_DIO0_OUT |  |
| 3 | 16 | GI_DAC_GI_DIO1_OUT |  |
| 3 | 17 | GI_DAC_GI_DIO2_OUT |  |
| 3 | 18 | GI_DAC_GI_DIO3_OUT |  |
| 3 | 19 | GI_DAC_GI_DIO4_OUT |  |
| 3 | 20 | GI_DAC_SCLK5 |  |
| 3 | 21 | GI_DAC_DOUT5 |  |
| 3 | 22 | GI_DAC_CONVST5 |  |
| 3 | 23 | GI_DAC_SCLK6 |  |
| 3 | 24 | GI_DAC_DOUT6 |  |
| 3 | 25 | GI_DAC_CONVST6 |  |
| 3 | 26 | GI_DAC_DIO5_IN |  |
| 3 | 27 | GI_DAC_DIO6_IN |  |

### NI USB-7856R

| BrightEyes-MCS USB | NI Connector | NI DIO | GI-BOX |
| --- | --- | --- | --- |
| SPAD0 | 0 (DIGITAL) | DIO 0 | SPAD_CONN |
| .. | 0 (DIGITAL) | ... | ... |
| SPAD24 | 0 (DIGITAL) | DIO 24 | SPAD_CONN |
| SPAD_ENABLE | 0 (DIGITAL) | DIO 25 | ENABLE |
| SPAD_SCLK | 0 (DIGITAL) | DIO 26 | VR0 |
| SPAD_SDATA | 0 (DIGITAL) | DIO 27 | VR1 |
| LASER_0 | 0 (DIGITAL) | DIO 28 | AUX0 |
| LASER_1 | 0 (DIGITAL) | DIO 29 | AUX1 |
| LASER_2 | 0 (DIGITAL) | DIO 30 | AUX2 |
| LASER_3 | 0 (DIGITAL) | DIO 31 | AUX3 |
|  |  |  |  |
| ANALOG_IN0 | 1 (ANALOG + DIG.) | AI 0 |  |
| ... | 1 (ANALOG + DIG.) | ... |  |
| ANALOG_OUT0 | 1 (ANALOG + DIG.) | AO 0 |  |
|  | 1 (ANALOG + DIG.) | ... |  |
| PIXEL_SYNC | 1 (ANALOG + DIG.) | DIO 5 |  |
| LINE_SYNC | 1 (ANALOG + DIG.) | DIO 6 |  |
| FRAME_SYNC | 1 (ANALOG + DIG.) | DIO 7 |  |
| AO_TRIGGER_TEST | 1 (ANALOG + DIG.) | DIO 8 |  |
| DET_EXTRA_0 | 1 (ANALOG + DIG.) | DIO 0 |  |
| DET_EXTRA_1 | 1 (ANALOG + DIG.) | DIO 1 |  |
| PIXEL_IN | 1 (ANALOG + DIG.) | DIO 10 |  |
| LASER_DEBUG | 1 (ANALOG + DIG.) | DIO 11 |  |
| LASER_0_BIS | 1 (ANALOG + DIG.) | DIO 12 |  |
| LASER_1_BIS | 1 (ANALOG + DIG.) | DIO 13 |  |
| LASER_2_BIS | 1 (ANALOG + DIG.) | DIO 14 |  |
| LASER_3_BIS | 1 (ANALOG + DIG.) | DIO 15 |  |

### NI PXIe-7856R

| BrightEyes-MCS USB | NI Connector | NI DIO | GI-BOX |
| --- | --- | --- | --- |
| SPAD0 | 1 (DIGITAL) | DIO 0 | SPAD_CONN |
| .. | 1 (DIGITAL) | ... | ... |
| SPAD24 | 1 (DIGITAL) | DIO 24 | SPAD_CONN |
| SPAD_ENABLE | 1 (DIGITAL) | DIO 25 | ENABLE |
| SPAD_SCLK | 1 (DIGITAL) | DIO 26 | VR0 |
| SPAD_SDATA | 1 (DIGITAL) | DIO 27 | VR1 |
| LASER_0 | 1 (DIGITAL) | DIO 28 | AUX0 |
| LASER_1 | 1 (DIGITAL) | DIO 29 | AUX1 |
| LASER_2 | 1 (DIGITAL) | DIO 30 | AUX2 |
| LASER_3 | 1 (DIGITAL) | DIO 31 | AUX3 |
|  |  |  |  |
| ANALOG_IN0 | 0 (ANALOG + DIG.) | AI 0 |  |
| ... | 0 (ANALOG + DIG.) | ... |  |
| ANALOG_OUT0 | 0 (ANALOG + DIG.) | AO 0 |  |
|  | 0 (ANALOG + DIG.) | ... |  |
| PIXEL_SYNC | 0 (ANALOG + DIG.) | DIO 5 |  |
| LINE_SYNC | 0 (ANALOG + DIG.) | DIO 6 |  |
| FRAME_SYNC | 0 (ANALOG + DIG.) | DIO 7 |  |
| AO_TRIGGER_TEST | 0 (ANALOG + DIG.) | DIO 8 |  |
| DET_EXTRA_0 | 0 (ANALOG + DIG.) | DIO 0 |  |
| DET_EXTRA_1 | 0 (ANALOG + DIG.) | DIO 1 |  |
| PIXEL_IN | 0 (ANALOG + DIG.) | DIO 10 |  |
| LASER_DEBUG | 0 (ANALOG + DIG.) | DIO 11 |  |
| LASER_0_BIS | 0 (ANALOG + DIG.) | DIO 12 |  |
| LASER_1_BIS | 0 (ANALOG + DIG.) | DIO 13 |  |
| LASER_2_BIS | 0 (ANALOG + DIG.) | DIO 14 |  |
| LASER_3_BIS | 0 (ANALOG + DIG.) | DIO 15 |  |

### GENOA INSTRUMENT — GI-BOX (PRISM)

| Connector | DIO | Label |
| --- | --- | --- |
| Connector | DIO | LABEL |
| C0 (Left) | DIO28 | AUX0 |
| C0 (Left) | DIO29 | AUX1 |
| C0 (Left) | DIO30 | AUX2 |
| C0 (Left) | DIO31 | AUX3 |
| C1 (Right) | DIO26 | AUX4 |
| C1 (Right) | DIO27 | AUX5 |
| C1 (Right) | DIO28 | AUX6 |
| C1 (Right) | DIO29 | AUX7 |
| C1 (Right) | DIO30 | AUX8 |
| C1 (Right) | DIO31 | AUX9 |
| C0 (Left) | DIO26 | VR0 |
| C0 (Left) | DIO27 | VR1 |
| C0 (Left) | DIO25 | ENABLE |
| C1 (Right) | DIO24 | SDA |
| C1 (Right) | DIO25 | SCL |
| C1 (Right) | ExtCLK | EXTCLK |

### GENOA INSTRUMENT — GI-DAC

| Label | DIO | Firmware Naming |
| --- | --- | --- |
| AO 0 | 0 | GI_DAC_SCLK0 |
|  | 1 | GI_DAC_SDIN0 |
|  | 2 | GI_DAC_SSYNC0 |
| AO 1 | 3 | GI_DAC_SCLK1 |
|  | 4 | GI_DAC_SDIN1 |
|  | 5 | GI_DAC_SSYNC1 |
| AO 2 | 6 | GI_DAC_SCLK2 |
|  | 7 | GI_DAC_SDIN2 |
|  | 8 | GI_DAC_SSYNC2 |
| AO 3 | 9 | GI_DAC_SCLK3 |
|  | 10 | GI_DAC_SDIN3 |
|  | 11 | GI_DAC_SSYNC3 |
| AO 4 | 12 | GI_DAC_SCLK4 |
|  | 13 | GI_DAC_SDIN4 |
|  | 14 | GI_DAC_SSYNC4 |
| DOUT | 15 | GI_DAC_GI_DIO0 |
|  | 16 | GI_DAC_GI_DIO1 |
|  | 17 | GI_DAC_GI_DIO2 |
|  | 18 | GI_DAC_GI_DIO3 |
|  | 19 | GI_DAC_GI_DIO4 |
| AI 0 | 20 | GI_DAC_SCLK5 |
|  | 21 | GI_DAC_DOUT5 |
|  | 22 | GI_DAC_CONVST5 |
| AI 1 | 23 | GI_DAC_SCLK6 |
|  | 24 | GI_DAC_DOUT6 |
|  | 25 | GI_DAC_CONVST6 |
| DIN | 26 | GI_DAC_DIO5 |
|  | 27 | GI_DAC_DIO6 |
| N.C. | 28 | GI_DAC_30 |
|  | 29 | GI_DAC_31 |
|  | 30 | GI_DAC_28 |
|  | 31 | GI_DAC_29 |

## Detector bit allocation

- [Bit used for each channel on the 7×7 SPAD](#bit-used-for-each-channel-on-the-77-spad)
- [Bit used for each channel on the 5×5 SPAD](#bit-used-for-each-channel-on-the-55-spad)

### Bit used for each channel on the 7×7 SPAD

| Channel | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 7 | 7 | 8 | 8 | 8 | 7 | 7 |
| 7 | 7 | 8 | 8 | 14 | 8 | 8 | 7 |
| 14 | 8 | 8 | 16 | 16 | 16 | 8 | 8 |
| 21 | 8 | 14 | 16 | 16 | 16 | 14 | 8 |
| 28 | 8 | 8 | 16 | 16 | 16 | 8 | 8 |
| 35 | 7 | 8 | 8 | 14 | 8 | 8 | 7 |
| 42 | 7 | 7 | 8 | 8 | 8 | 7 | 7 |


### Bit used for each channel on the 5×5 SPAD

| Channel | 0 | 1 | 2 | 3 | 4 |
| --- | --- | --- | --- | --- | --- |
| 0 | 4 | 4 | 4 | 4 | 4 |
| 5 | 4 | 5 | 6 | 5 | 4 |
| 10 | 4 | 6 | 12 | 6 | 4 |
| 15 | 4 | 5 | 6 | 5 | 4 |
| 20 | 4 | 4 | 4 | 4 | 4 |

## Channel numbering

The following tables describe the same physical 7×7 SPAD array using four numbering schemes. Rows and columns retain the same physical orientation in every table; only the channel labels change.

- [A: BrightEyes-MCS software numbering](#a-brighteyes-mcs-software-numbering)
- [B: Firmware pinout numbering](#b-firmware-pinout-numbering)
- [C: GI SPAD numbering](#c-gi-spad-numbering)
- [D: Legacy firmware numbering](#d-legacy-firmware-numbering)

Notation legend:

| Notation | Numbering scheme | Range | Definition |
|----------|------------------|-------|------------|
| A | BrightEyes-MCS software | 0–48 | Zero-based row-major order, from the top-left channel to the bottom-right channel. |
| B | Firmware pinout | 0–48 | Zero-based pinout order: the inner 5×5 channels are numbered 0–24 and the outer ring 25–48 because they use different connectors. |
| C | GI SPAD 7×7 | 1–49 | One-based row-major order; each value is the corresponding A value plus 1. |
| D | Legacy firmware | 1–49 | One-based legacy pinout order; each value is the corresponding B value plus 1. |

### A: BrightEyes-MCS software numbering

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 | 32 | 33 | 34 |
| 35 | 36 | 37 | 38 | 39 | 40 | 41 |
| 42 | 43 | 44 | 45 | 46 | 47 | 48 |

### B: Firmware pinout numbering

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- |
| 25 | 26 | 27 | 28 | 29 | 30 | 31 |
| 32 | 0 | 1 | 2 | 3 | 4 | 33 |
| 34 | 5 | 6 | 7 | 8 | 9 | 35 |
| 36 | 10 | 11 | 12 | 13 | 14 | 37 |
| 38 | 15 | 16 | 17 | 18 | 19 | 39 |
| 40 | 20 | 21 | 22 | 23 | 24 | 41 |
| 42 | 43 | 44 | 45 | 46 | 47 | 48 |

### C: GI SPAD numbering

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| 8 | 9 | 10 | 11 | 12 | 13 | 14 |
| 15 | 16 | 17 | 18 | 19 | 20 | 21 |
| 22 | 23 | 24 | 25 | 26 | 27 | 28 |
| 29 | 30 | 31 | 32 | 33 | 34 | 35 |
| 36 | 37 | 38 | 39 | 40 | 41 | 42 |
| 43 | 44 | 45 | 46 | 47 | 48 | 49 |

### D: Legacy firmware numbering

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- |
| 26 | 27 | 28 | 29 | 30 | 31 | 32 |
| 33 | 1 | 2 | 3 | 4 | 5 | 34 |
| 35 | 6 | 7 | 8 | 9 | 10 | 36 |
| 37 | 11 | 12 | 13 | 14 | 15 | 38 |
| 39 | 16 | 17 | 18 | 19 | 20 | 40 |
| 41 | 21 | 22 | 23 | 24 | 25 | 42 |
| 43 | 44 | 45 | 46 | 47 | 48 | 49 |

## DFD frequency

| Setting | 12M100 | 37M122 | 40M91 | 80M91 | Notes |
| --- | --- | --- | --- | --- | --- |
| DFD Bins | 100 | 122 | 91 | 91 |  |
| Excitation Freq. (MHz) | 12 | 36.666665999999999 | 40 | 80 | = Sequencer Freq. (MHz) |
| Excitation "fast" Freq. (MHz) | 144 | 219.99999600000001 | 240 | 240 | = Sequencer Bin Freq. (MHz) |
| Window Freq. (MHz) | 400 | 406.66666666600003 | 404.44444443999998 | 404.44444443999998 | = Fastest Freq. Available (MHz) |
| Ratio  | 12 | 6 | 6 | 6 | = Number of bins available on the Laser Sequencer) |
| Sampling Freq. (MHz) | 12.121212 | 36.969696969696898 | 40.444444443999998 | 80.888888879999996 |  |
| Frequency differences | 0.12121199999999988 | 0.30303096969689847 | 0.44444444399999838 | 0.88888887999999611 |  |
| Histogram completation time (us) | 8.2500082500082588 | 3.2999927400167475 | 2.2500000022500082 | 1.1250000112500051 |  |
