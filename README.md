# qb-target-examine-vehicle

![image](https://user-images.githubusercontent.com/11475502/130977964-f1aed865-ce4b-4006-928b-66ff963f16fc.png)

Dependencies
1. qb-mechanicjob
2. qb-menu
3. qb-target

Add this at the very bottom of your qb-mechanicjob > client > main.lua
```
RegisterNetEvent('CheckVehStatus')
AddEventHandler('CheckVehStatus', function()
    veh = QBCore.Functions.GetClosestVehicle()
    plate = GetVehicleNumberPlateText(veh)
    engineHealth = GetVehicleEngineHealth(veh)
    vehTemp = GetVehicleEngineTemperature(veh)
    bodyHealth = GetVehicleBodyHealth(veh)
    fuelHealth = exports['LegacyFuel']:GetFuel(veh)
    tankHealth = GetVehiclePetrolTankHealth(veh)
    exports['qb-menu']:openMenu({
        {
            id = 1,
            header = "<  Go back",
            txt = "",
            params = {
                event = "nh-context:closeMenu"
            }
        },
        {
            id = 2,
            header = "Fuel Level",
            txt = "Status: " .. round(fuelHealth) .. ".0% / 100.0%",
        },
        {
            id = 3,
            header = "Engine Health",
            txt = "Status: " .. round(engineHealth) / 10 .. "% / 100.0%",
        },
        {
            id = 4,
            header = "Body Health",
            txt = "Status: " .. round(bodyHealth) / 10 .. "% / 100.0%",
        },
        {
            id = 5,
            header = "Tank Health",
            txt = "Status: " .. round(tankHealth) / 10 .. "% / 100.0%",
        },
        {
            id = 6,
            header = "Engine Temperature",
            txt = "Status: " .. round(vehTemp) .. "° C",
        },        
    })
end)
```

Attach this to your preferred options section of your qb-target config.lua
```
type = "client",
event = "CheckVehStatus",
icon = "fas fa-wrench",
label = "Examine Vehicle",
```
