# Installation instructions for hgail
- Initially written by Derek in Jan 2nd week
- Added to by Raunak on Jan 25
- Predependency: [ngsim_env](https://github.com/wulfebw/ngsim_env)

## Here are the instructions
```bash
cd ~
git clone https://github.com/wulfebw/hgail
source activate rllab3
cd hgail
python setup.py develop
cd tests python runtests.py
cd ~/ngsim_env
mkdir data
mkdir data/trajectories
mkdir data/experiments
cd scripts
julia
  >> Pkg.checkout("AutomotiveDrivingModels", "lidar_sensor_optimization")
  >> quit()

##Get the data
cd ~/.julia/v0.6/NGSIM/data
wget https://github.com/sisl/NGSIM.jl/releases/download/v1.0.0/data.zip
unzip data.zip

##Fix a trajectory converstion script
cd ../src
#change line 205 of .julia/v0.6/NGSIM/src/trajdata.jl" to outpath = Pkg.dir("NGSIM", "data", "trajdata_"*splitdir(filename)[2])

##Create trajectories from the data
cd ../data
julia
  >> using NGSIM
  >> convert_raw_ngsim_to_trajdatas()
  >> quit()

cd ~/ngsim_env/scripts

julia extract_ngsim_demonstrations.jl
cd imitation
python imitate.py [options here]
```
See installation log ![logFile]
