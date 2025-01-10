# FLOORPLANNING

`run_floorplan`

.def (design exchange format) file in `/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/<recent_run>/results/floorplans`
`less picorv32a.floorplan.def`

<img width="440" alt="Screenshot 2024-11-19 at 7 29 29 PM" src="https://github.com/user-attachments/assets/c9063ed4-a611-4214-94db-604cce1833d9">

`magic -T /Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def`

<img width="682" alt="Screenshot 2024-11-19 at 7 31 58 PM" src="https://github.com/user-attachments/assets/5fb5f6bc-be8f-4011-965a-5a03384d1eef">

---

## keys to use in magic

`s` -> select
`v` -> fit layout on screen
`left mouse, right mouse` -> select
`z` -> zoom
arrow keys -> move layout

<img width="1012" alt="Screenshot 2024-11-19 at 7 34 29 PM" src="https://github.com/user-attachments/assets/1e69dba8-a58b-4ae7-9329-f1a65f53ba6d">

`what` in tcon window for information about selected cell

<img width="1120" alt="Screenshot 2024-11-19 at 7 34 53 PM" src="https://github.com/user-attachments/assets/1bf90819-e6b3-4451-8e5d-60e199d98a5a">

---

## Run placement

`run_placement`

[image_here]

```
/Desktop/work/tools/openlane_working dir/openlane/designs/picorv32a/runs/<recent_run>/results/placements/
`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs. tech/magic/sky130A.tech lef read ../../tmp/merged. lef def read picorv32a.placement.def
```

[image_here]

---
