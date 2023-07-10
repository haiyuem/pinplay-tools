# Instructions and change log
pinplay-scripts is used together with Intel PIN SDE kit to generate representative regions for applications that are too long to profile in whole. 

Using pinpoint.py with ./pin should be possible but I was stuck, future investigations pending. 

## Usage for sde_pinpoint.py:
Launch command in the results directory. 
Example command: python3 sde_pinpoints.py --command="/bin/ls" --program_name="ls" --input_name="test3" --sdehome="/home/hm2595/pintool/sde-external-9.21.1-2023-04-24-lin"  --mode=st --default_phase --slice_size="10000"

command: run command 
program_name/input_name: can be whatever, these are used to distinguish different runs of the same command 
mode: st=single thread, can be multiple threads (mt)
default_phase: generate basic block vectors, run simpoint to find the representative regions, replay(?) -- TODO: will fail after replay

Or use config file to run: python3 pinpoints.py --default_phases rundir/vision.cfg 

Results: Look at *.Data folder, *.bb files are the basic block vectors (input files for simpoint), *.csv is the final output that we care about. Look for the highest weight and the corresponding region is the most representative region.

python3 pinpoints.py --help for help 

# -----ORIGINAL README-----

Pin Record/Replay Tools

A collection of C/C++ programs and Python scripts to be used in conjunction with Intel Software Development Emulator (Intel SDE, available externally separately). The purpose is to use record/replay functionality in SDE for program analysis.


 ├── openmp
 ├── Examples
 ├── GlobalLoopPoint
 └── pinplay-scripts

openmp: Test OpenMP program sources, makefile, shell-scripts to run looppoint toolchain.

Examples:Test program sources and  makefile for building simple SDE+PinPlay tools

GlobalLoopPoint: sources for tools doing global profiling of multi-threaded programs to find representative simulation regions.

  See the HPCA-2022 paper:
  LoopPoint: Checkpoint-driven Sampled Simulation for Multi-threaded Applications
Alen Sabu (National University of Singapore), Harish Patil, Wim Heirman (Intel), Trevor E. Carlson (National University of Singapore)

pinplay-scripts: Python scripts to automate simulation region selection for SDE-based single threaded and multi-threaded programs.
