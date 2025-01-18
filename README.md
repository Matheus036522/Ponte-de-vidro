local segmentSystem = workspace:FindFirstChild("segmentSystem")
if not segmentSystem then
    warn("segmentSystem is not on workspace")
    return
end
print("segmentSystem found")

local segmentsFolder = segmentSystem:FindFirstChild("Segments")
if not segmentsFolder then
    warn("Segments not found in segmentSystem")
    return
end
print("folder Segments found")

-- Iterate over all the segments (Segment1, Segment2, etc.)
for _, segment in ipairs(segmentsFolder:GetChildren()) do
    if segment:IsA("Model") then
        print("Exploring segment (Model): " .. segment.Name)

        local folder = segment:FindFirstChild("Folder") -- Check if a "Folder" exists in each Model
        if folder then
            print("'Folder' found in " .. segment.Name)

            -- Iterate over all children of the Folder
            for _, child in ipairs(folder:GetChildren()) do
                if child:IsA("Part") then
                    print("Part detected: " .. child.Name)

                    -- Check if the Part has exactly 3 children
                    local childrenCount = #child:GetChildren()
                    print("Part " .. child.Name .. " has " .. childrenCount .. " children")

                    if childrenCount == 3 then
                        print("Deleting the Part: " .. child.Name)
                        child:Destroy() -- Delete the Part on the client side
                    end
                end
            end
        else
            print("No 'Folder' found in " .. segment.Name)
        end
    else
        print(segment.Name .. " is not a Model, ignored")
    end
end
