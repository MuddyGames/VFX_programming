# Blender Motion Tracking Guide

Blender camera tracking: placing 3D objects into real-world footage and fixing mesh sliding.

**13 steps, from importing footage to final compositing.**

## Contents

1. [Import Your Footage](#step-1-import-your-footage)
2. [Add Tracking Markers](#step-2-add-tracking-markers)
3. [Track Your Markers](#step-3-track-your-markers)
4. [Clean Up Your Tracking Data](#step-4-clean-up-your-tracking-data)
5. [Solve Camera Motion](#step-5-solve-camera-motion)
6. [Set the Floor, Origin and Scene Scale](#step-6-set-the-floor-origin-and-scene-scale)
7. [Set Up the Tracking Scene](#step-7-set-up-the-tracking-scene)
8. [Add and Position Your 3D Mesh](#step-8-add-and-position-your-3d-mesh)
9. [Fix Mesh Sliding: Add More Tracking Markers](#step-9-fix-mesh-sliding-add-more-tracking-markers)
10. [Check Mesh Depth and Placement](#step-10-check-mesh-depth-and-placement)
11. [Check Focal Length and Tracking Accuracy](#step-11-check-focal-length-and-tracking-accuracy)
12. [Check Tracking Stability Throughout the Footage](#step-12-check-tracking-stability-throughout-the-footage)
13. [Final Compositing and Rendering](#step-13-final-compositing-and-rendering)

---

## Step 1: Import Your Footage

**Goal:** Prepare your footage for motion tracking.

1. Open Blender.
2. Select the **Motion Tracking** workspace.
3. Open the **Movie Clip Editor**.
4. Click **Open** and load your video.

<!-- IMAGE: images/motion_tracking/open_movie_clip.png -->

5. Match the scene frame rate to your footage in **Output Properties → Format → Frame Rate**.

![Setting the output frame rate](images/motion_tracking/setting_output_frame_rate.png)

6. Set the correct frame range. In the Movie Clip Editor sidebar (`N`), open the **Footage Settings** panel and click **Set Scene Frames**. This sets the scene's start and end frames to match the clip's length.

![Set Scene Frames in the Movie Clip Editor](images/motion_tracking/set_scene_frames.png)

   Check the result under **Output Properties → Frame Range**.

### Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Alt + O` | Open clip (where supported) |
| `Space` | Play / pause |
| `Left` / `Right Arrow` | Previous / next frame |
| `Shift + Left Arrow` | First frame |
| `Shift + Right Arrow` | Last frame |

> 💡 **Tip:** Use footage with minimal motion blur and plenty of visible environmental detail.

---

## Step 2: Add Tracking Markers

**Goal:** Give Blender points to follow throughout the footage.

1. Find clearly visible details in your footage.
2. Place your mouse over a feature.
3. Press `Ctrl + Left Click` to add a tracking marker.
4. Position it accurately over the feature.
5. Start with approximately **8 to 15** reliable markers.
6. Distribute markers across the foreground, middle ground and background.
7. Include markers near the surface where your 3D mesh will sit.

<!-- IMAGE: images/motion_tracking/adding_tracking_markers.png -->

### Good tracking points

- Building corners
- Pavement cracks
- Floor patterns
- Window corners
- Static furniture

### Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + Left Click` | Add marker |
| `X` | Delete selected marker |

> 💡 **Tip:** Track stationary environmental features, **not** moving people or vehicles.

---

## Step 3: Track Your Markers

**Goal:** Follow the selected features throughout the video.

1. Select your tracking markers.
2. Press `Ctrl + T` to track forwards.
3. Let Blender track through the footage.
4. Inspect the markers as they move.
5. Stop when a marker starts slipping.
6. Correct the marker or remove it if necessary.
7. Track backwards where required.

<!-- IMAGE: images/motion_tracking/tracking_markers.png -->

### Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + T` | Track forwards |
| `Ctrl + Shift + T` | Track backwards |

> ⚠️ **Important:** Don't assume a track is good just because Blender successfully tracked it. Make sure it stays attached to its original feature.

---

## Step 4: Clean Up Your Tracking Data

**Goal:** Remove inaccurate tracking information before solving the camera.

1. Scrub through the footage.
2. Identify markers drifting away from their original features.
3. Check markers that become obscured.
4. Look for markers following moving objects.
5. Correct inaccurate tracks.
6. Delete unreliable markers.
7. Check that your remaining markers are distributed across the image.

<!-- IMAGE: images/motion_tracking/cleaning_tracking_data.png -->

> 💡 **Tip:** A smaller number of accurate tracks is better than a large number of inaccurate tracks.
>
> 💡 **Tip:** Bad tracking data can harm your camera solve and contribute to problems such as mesh sliding.

---

## Step 5: Solve Camera Motion

**Goal:** Reconstruct the movement of your real camera in 3D space.

1. Open the **Solve** panel.
2. Check the camera's focal length.
3. Set appropriate **Keyframe A** and **Keyframe B** positions.
4. Enable **Refine Focal Length** if necessary.
5. Click **Solve Camera Motion**.
6. Wait for Blender to calculate the camera movement.
7. Review the **Average Solve Error**.

<!-- IMAGE: images/motion_tracking/solve_camera_motion.png -->

> 💡 **Tip:** A lower solve error is generally better, but it doesn't guarantee that your mesh will stay perfectly attached to the real-world surface.
>
> 💡 **Tip:** Don't ignore poor tracking markers just to get a lower error. It's a balance between a low error, the number of markers and the quality of the camera solve.

---

## Step 6: Set the Floor, Origin and Scene Scale

**Goal:** Establish the correct orientation and scale of your reconstructed environment.

1. Select three tracking points on the same flat surface.
2. Open the **Solve** panel.
3. Click **Set Floor**.
4. Select a tracking marker where you want the scene origin.
5. Click **Set Origin**.
6. Select two points with a known real-world distance.
7. Click **Set Scale**.
8. Enter the actual distance.

<!-- IMAGE: images/motion_tracking/set_floor_origin_scale.png -->

> ⚠️ **Important:** Your floor markers must be on the same physical plane. Don't mix points from the floor and walls. This step is particularly important when placing a mesh on a real-world surface; otherwise it will hop or jitter.

---

## Step 7: Set Up the Tracking Scene

**Goal:** Create the 3D camera and background setup.

1. Open the **Scene Setup** panel.
2. Click **Setup Tracking Scene**.
3. Switch to the **3D Viewport**.
4. Press `Numpad 0` to view through the tracked camera.
5. Inspect the reconstructed scene.
6. Confirm that the camera movement matches your original footage.

<!-- IMAGE: images/motion_tracking/setup_tracking_scene.png -->

Blender creates the camera and background setup needed for compositing.

---

## Step 8: Add and Position Your 3D Mesh

**Goal:** Place your 3D object into the reconstructed environment.

1. Move your cursor into the **3D Viewport**.
2. Press `Shift + A`.
3. Select the mesh you want to add.
4. Position it on the reconstructed surface.
5. Adjust its height.
6. Match its rotation to the real-world surface.
7. Adjust its scale.
8. Check its position through the tracked camera using `Numpad 0`.

<!-- IMAGE: images/motion_tracking/positioning_mesh.png -->

### Useful shortcuts

| Shortcut | Action |
|---|---|
| `Shift + A` | Add object |
| `G` | Move |
| `R` | Rotate |
| `S` | Scale |
| `Ctrl + A` | Apply transforms |
| `Numpad 0` | Camera view |
| `Numpad .` | Frame selected |

> 💡 **Important:** If your mesh is attached to a stationary surface, its position in the reconstructed 3D world should remain fixed.

---

## Step 9: Fix Mesh Sliding: Add More Tracking Markers

**Goal:** Improve the camera solve if too little or poorly distributed tracking data is causing sliding.

1. Find the exact frame where your mesh starts sliding.
2. Pause the footage.
3. Inspect your existing tracking markers.
4. Add new markers around the affected area.
5. Add more markers across the foreground and background.
6. Make sure they follow stationary real-world features.
7. Track the new markers forwards and backwards.
8. Inspect their accuracy.
9. Remove unreliable markers.
10. Solve the camera motion again.

<!-- IMAGE: images/motion_tracking/adding_more_markers.png -->

> 💡 **Recommendation:** Add reliable markers throughout the sequence, not just at the frame where sliding begins.

More accurate tracking data can improve the camera reconstruction. Adding more markers won't automatically fix every sliding problem, but it's a good start.

---

## Step 10: Check Mesh Depth and Placement

**Goal:** Make sure your mesh is positioned correctly in 3D space.

An incorrectly reconstructed depth can make your mesh appear to slide as the camera moves.

1. Select your mesh.
2. Inspect its position in the **3D Viewport**.
3. Check its distance from the tracked camera.
4. Confirm that its bottom aligns with the intended surface.
5. Check that the reconstructed floor is correctly oriented.
6. Adjust the mesh position if necessary.
7. Replay the footage to check the result.

<!-- IMAGE: images/motion_tracking/checking_mesh_depth.png -->

> 💡 **Tip:** If the mesh looks correct at first but drifts as the camera moves, investigate the camera solve and scene reconstruction before manually animating the mesh.

---

## Step 11: Check Focal Length and Tracking Accuracy

**Goal:** Identify camera settings and tracking errors that may contribute to sliding.

### Check focal length

1. Open the **Solve** panel.
2. Check your camera's focal length.
3. Enable **Refine Focal Length** if appropriate.
4. Solve the camera again.
5. Compare the results.

<!-- IMAGE: images/motion_tracking/focal_length_settings.png -->

### Check lens distortion

1. Inspect the original footage.
2. Look for curved lines near the image edges.
3. Check the camera distortion settings.
4. Refine distortion parameters if necessary.
5. Repeat the solve.

<!-- IMAGE: images/motion_tracking/lens_distortion_settings.png -->

### Check individual markers

1. Find the frame where sliding begins.
2. Inspect the tracking markers.
3. Look for markers that have slipped.
4. Correct their positions.
5. Remove unreliable tracks.
6. Solve again.

---

## Step 12: Check Tracking Stability Throughout the Footage

**Goal:** Confirm that your mesh stays attached to the intended surface.

**Don't judge your tracking from just one frame!** Check:

- [ ] The first frame
- [ ] The frame where sliding begins
- [ ] A frame in the middle
- [ ] The last frame
- [ ] The complete sequence, played back
- [ ] That the mesh remains attached to the intended surface

<!-- IMAGE: images/motion_tracking/checking_stability.png -->

### Additional techniques

- Adjust tracking weights where appropriate.
- Remove unreliable tracking markers.
- Check the tracking motion model.
- Investigate camera distortion.
- Check your reconstructed floor and scene scale.

> 💡 **Tip:** Don't use manual keyframes to compensate for an inaccurate camera solve.

---

## Step 13: Final Compositing and Rendering

**Goal:** Finish the scene and produce the final result.

1. Add materials to your mesh.
2. Set up lighting that matches the original footage.
3. Add shadows where appropriate.
4. Check that the mesh has the correct scale.
5. Verify alignment throughout the footage.
6. Set up the **Compositor**.
7. Combine the rendered 3D scene with your original footage.
8. Check the final result.
9. Render your animation.

<!-- IMAGE: images/motion_tracking/compositor_setup.png -->
<!-- IMAGE: images/motion_tracking/final_render.png -->