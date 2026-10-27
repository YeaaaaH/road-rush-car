# C-001: Motor bracket in FreeCAD (first CAD part)
**Status:** todo
**Depends on:** FreeCAD installed. Chassis track: independent of the firmware tasks

## Goal
The user models the motor bracket themselves to refresh their CAD skills. Claude sets the requirements, gives hints and reviews. The user shares a link to the model, and the review is done together from it.

## Done when
- [ ] Measured as the model needs them (record in `docs/bom.md`): N20 motor body and mounting holes, drive wheel diameter and width, caster type, full height and mounting holes
- [ ] Printer model and filament known
- [ ] Fully constrained sketch (Sketcher), solid built in Part Design
- [ ] Mounting holes with FDM clearance (M3 → 3.2–3.4 mm)
- [ ] Axle height matches the chosen base plate height (see the spacer formula in `../CLAUDE.md`)
- [ ] Both axles coaxial and parallel to the base (the wooden rig pulls to one side because they aren't)
- [ ] Print orientation chosen so the load doesn't split layers
- [ ] Test print fits the motor; any corrections logged here

## Notes / log
