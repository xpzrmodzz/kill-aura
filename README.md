local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Variable de contrôle pour activer ou désactiver le script
local G_ = true  -- true pour démarrer le script, false pour le détruire

-- Définir les arguments
local args = {
    ["multiply"] = 1,
    ["action"] = "hit",
}

-- Fonction pour appliquer l'action à un joueur
local function applyActionToPlayer(player)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        args.enemyHum = player.Character.Humanoid
        ReplicatedStorage:WaitForChild("DamageEvent"):FireServer(args)
    end
end

-- Boucle principale du script
while true do
    -- Vérifier si G_ est toujours vrai avant chaque itération de la boucle
    if G_ then
        -- Parcourir tous les joueurs, excluant le joueur local, et appliquer l'action à chacun d'eux
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= Players.LocalPlayer then
                applyActionToPlayer(player)
            end
        end
        -- Attendre un court instant avant de vérifier à nouveau les joueurs
        wait(1)
    else
        -- Si G_ est devenu faux, détruire le script et terminer l'exécution
        script:Destroy()
        break
    end
end
