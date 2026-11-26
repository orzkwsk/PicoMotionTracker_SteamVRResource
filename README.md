# PICO tracker display resources

Resource-only OpenVR package. Register the directory containing
`driver.vrdrivermanifest` with SteamVR. Its namespace is `pico_tracker_assets`.
`display-resources.json` contains the optional public display descriptor;
applications must explicitly publish it using a compatible protocol version.

## Editing

- `sources/models/pico_motion_tracker.step`: complete editable CAD, in mm, with
  four solids. `sources/models/parts/` contains the separate housing, button,
  LED lens and USB tongue STEP files. Edit these in a STEP-capable CAD tool.
- `resources/rendermodels/pico_motion_tracker/`: static OBJ/MTL/PNG, in metres.
  Reuses the project's existing processed identification model, with its existing
  model-local orientation, UVs and texture. Renaming does not alter its geometry.
  Keep the directory, OBJ, MTL and texture basenames identical and update their
  internal references together. CAD edits require re-exporting the runtime mesh;
  keep the expanded position/UV/normal vertex count within OpenVR's index limit.
- `resources/icons/`: supplied 64px PNG/GIF files, unchanged. Keep `@2x` in their
  names. These are the original supplied images, without modifications.

The icons cover Ready, Searching, Standby, Off and NotReady. The dedicated
NotReady image is a byte-identical copy of the supplied grey Off icon for the
initial waiting state. SearchingAlert and StandbyAlert also use this grey image
so waiting with a tracking warning retains the supplied tracker appearance.
Other states use the output adapter's defaults.
The Searching GIF has 30 frames and uses edge colours
matched to background `#202225`; its appearance can differ on other backgrounds.

After replacing resources, use new references or restart the output Provider
according to its resource-cache rules.

## Updates

Publish `main` as one complete root-commit snapshot, without retaining parent
commits. Review the complete staged tree and use `--force-with-lease` against
the previously observed remote SHA. Update the consuming project's submodule
SHA with a normal commit; never rewrite the consuming project's history.
