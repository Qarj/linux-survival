# StableSwarmUI

```sh
conda activate lc
cd $HOME/git/StableSwarmUI
rl
./launch-linux.sh
```

The rl command will reset the video card. Must be done after waking computer from sleep.

Ensure only one browser tab is opening pointing to `http://localhost:7801/Text2Image`.

Get safetensors models from Hugging Face.

Also civitai.com:

-   sign in with Google
-   go to the "Models" tab
-   select Most Downloaded on the right
-   select the filter "All time"
-   select the filter File format "SafeTensor"
-   select the base model "SDXL 1.0"

Top downloaded model should be something like Juggernaut XL.

Download models and put them in `~/git/StableSwarmUI/models`.
