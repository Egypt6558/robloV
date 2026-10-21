local Translations = {
    ["Home"] = "主页",
    ["Server"] = "服务器",
    ["MISC"] = "杂项",
    ["VIREX · V1"] = "VIREX · V1",
    ["VISUAL"] = "视觉",
    ["COMBAT"] = "战斗",
    ["UNLOCK"] = "解锁",
    ["WORLD"] = "世界",
    ["IMMORTAL"] = "无敌",
    ["CONFIG"] = "设置",
    ["视野范围"] = "视野范围",
    ["Camera FOV"] = "相机视野",
    ["Character"] = "角色",
    ["Infinite Jump"] = "无限跳跃",
    ["旋转"] = "旋转",
    ["VIREX Immortal"] = "VIREX 无敌",
    ["Accuracy"] = "精准度",
    ["Randomize Accuracy"] = "随机精准度",
    ["Auto Ability"] = "自动技能",
    ["Keyboard"] = "键盘",
    ["Triggerbot"] = "自瞄触发",
    ["DETECTION"] = "检测",
    ["无限"] = "无限",
    ["死亡刀片"] = "死亡刀片",
    ["时间洞"] = "时间洞",
    ["Slashes Of Fury"] = "狂怒斩击",
    ["幽灵"] = "幽灵",
    ["ABILITY ESP"] = "技能透视",
    ["Ability ESP"] = "技能透视",
    ["BALL STATISTIC"] = "球体统计",
    ["Ball Statistic"] = "球体统计",
    ["NO RENDER"] = "关闭渲染",
    ["No Render"] = "关闭渲染",
    ["EMOTES"] = "表情",
    ["表情符号"] = "表情符号",
    ["Auto Stop"] = "自动停止",
    ["Emote Type"] = "表情指令",
    ["/e dance"] = "/e dance",
    ["Jump Power"] = "跳跃力度",
    ["Jump Power Value"] = "跳跃力度数值",
    ["Gravity"] = "重力",
    ["Gravity Value"] = "重力数值",
    ["Hip Height"] = "臀部高度",
    ["Hip Height Value"] = "臀部高度数值",
    ["CUSTOMIZE"] = "自定义",
    ["STATIC"] = "静态",
    ["MOTION"] = "动态",
    ["FONTS"] = "字体",
    ["COLORS"] = "颜色",
    ["STATIC BACKGROUNDS"] = "静态背景",
    ["NOIR"] = "暗夜",
    ["ICE"] = "冰霜",
    ["VIOLET"] = "紫罗兰",
    ["CRIMSON"] = "绯红",
    ["MINT"] = "薄荷",
    ["SUNSET"] = "落日",
    ["VOID"] = "虚空",
    ["AUTO PARRY"] = "自动弹反",
    ["Auto Parry"] = "自动弹反",
    ["Parry Mode"] = "弹反模式",
    ["Remote"] = "远程",
    ["CURVE UI"] = "曲线UI",
    ["Curve UI"] = "曲线UI",
    ["Random Curve"] = "随机曲线",
    ["Unlock All"] = "全部解锁",
    ["SKY CHANGER"] = "天空修改",
    ["Sky Changer"] = "天空修改器",
    ["Sky Preset"] = "天空预设",
    ["Sunset"] = "落日",
    ["旋转 Speed"] = "旋转速度",
    ["Walk Speed"] = "移速",
    ["Walk Speed Value"] = "移速数值",
    ["自动弹反"] = "自动弹反",
     ["弹反模式"] = "弹反模式",
     ["KEYPRESS"] = "按键触发",
     ["KEYBOARD"] = "键盘设置",
     ["键盘"] = "键盘",
     ["TRIGGERBOT"] = "自瞄触发",
     ["自瞄触发"] = "自瞄触发",
     ["检测"] = "检测",
     ["无限"] = "无限",
     ["AUTO SPAM"] = "自动连击",
     ["Auto Spam"] = "自动连击",
     ["Spam Mode"] = "连击模式",
     ["Animation Fix"] = "动画修复",
     ["Spam Rate"] = "连击速率",
     ["MANUAL SPAM"] = "手动连击",
     ["Show Spam Button"] = "显示连击按钮",
     ["KEYPRESS"] = "按键触发"
}

local function translateText(text)
    if not text or type(text) ~= "string" then return text end
    
    if Translations[text] then
        return Translations[text]
    end
    
    for en, cn in pairs(Translations) do
        if text:find(en) then
            return text:gsub(en, cn)
        end
    end
    
    return text
end

local function setupTranslationEngine()
    local success, err = pcall(function()
        local oldIndex = getrawmetatable(game).__newindex
        setreadonly(getrawmetatable(game), false)
        
        getrawmetatable(game).__newindex = newcclosure(function(t, k, v)
            if (t:IsA("TextLabel") or t:IsA("TextButton") or t:IsA("TextBox")) and k == "Text" then
                v = translateText(tostring(v))
            end
            return oldIndex(t, k, v)
        end)
        
        setreadonly(getrawmetatable(game), true)
    end)
    
    if not success then
        warn("元表劫持失败:", err)
       
        local translated = {}
        local function scanAndTranslate()
            for _, gui in ipairs(game:GetService("CoreGui"):GetDescendants()) do
                if (gui:IsA("TextLabel") or gui:IsA("TextButton") or gui:IsA("TextBox")) and not translated[gui] then
                    pcall(function()
                        local text = gui.Text
                        if text and text ~= "" then
                            local translatedText = translateText(text)
                            if translatedText ~= text then
                                gui.Text = translatedText
                                translated[gui] = true
                            end
                        end
                    end)
                end
            end
            
            local player = game:GetService("Players").LocalPlayer
            if player and player:FindFirstChild("PlayerGui") then
                for _, gui in ipairs(player.PlayerGui:GetDescendants()) do
                    if (gui:IsA("TextLabel") or gui:IsA("TextButton") or gui:IsA("TextBox")) and not translated[gui] then
                        pcall(function()
                            local text = gui.Text
                            if text and text ~= "" then
                                local translatedText = translateText(text)
                                if translatedText ~= text then
                                    gui.Text = translatedText
                                    translated[gui] = true
                                end
                            end
                        end)
                    end
                end
            end
        end
        
        local function setupDescendantListener(parent)
            parent.DescendantAdded:Connect(function(descendant)
                if descendant:IsA("TextLabel") or descendant:IsA("TextButton") or descendant:IsA("TextBox") then
                    task.wait(0.1)
                    pcall(function()
                        local text = descendant.Text
                        if text and text ~= "" then
                            local translatedText = translateText(text)
                            if translatedText ~= text then
                                descendant.Text = translatedText
                            end
                        end
                    end)
                end
            end)
        end
        
        pcall(setupDescendantListener, game:GetService("CoreGui"))
        local player = game:GetService("Players").LocalPlayer
        if player and player:FindFirstChild("PlayerGui") then
            pcall(setupDescendantListener, player.PlayerGui)
        end
        
        while true do
            scanAndTranslate()
            task.wait(3)
        end
    end
end

task.wait(2)

setupTranslationEngine()

local success, err = pcall(function()
loadstring(game:HttpGet("https://cdn.luaprotect.dev/u/8660b0/vvrjsVBtDuZWVD_9"))()

end)

if not success then
    warn("加载失败:", err)
end
