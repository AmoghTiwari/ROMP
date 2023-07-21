main.py
    seq.inference
        image backbone
        motion backbone
        temp_head_forward
            temporal_head
                TRACE_head (in trace2/models/model.py)
                    extract_temporal_features
                        self.temp_model -> ConvGRU
                        DeformConv
                        A few things are happenning here. Have a look
                    inference_regression (inputs are the temporal feature maps and regular OF maps)
                        coarse2finelocalization
                        if flow is not None, combine (concatenate) flow and feature_maps
                        mesh_feature_map -> From the above combined_map

Level-1: 
    Extract image features from image backbone (HR-Net) -> F
    Extract OF features from OF backbone (RAFT)

Level-2: 
    Obtain temporally aware image features from F using a ConvGRU followed by a few other steps -> F'

Level-3:
    coarse2finelocalization (Same as BEV)
    combined_feature_maps (concatenate flow and temporally aware features)
    mesh_feature_maps (from combined feature maps)
    motion_regression (using combined feature maps) to get motion offsets
    -> Another head for cam motion and rotation maps
    -> 
    perform_tracking [Function comes from .TempTracker] (a few things happen before this)
    prepare_complete_trajectory_features_withmemory
    -> Further smoothening

