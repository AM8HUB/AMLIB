# 🎨 Modern UI Library V2

Uma biblioteca de interface (UI) para Roblox minimalista, moderna e totalmente animada. Agora conta com **Sistema de Configuração (Save/Load)** automático e **Barra de Pesquisa**.

## ✨ Funcionalidades

- **Design Premium:** Tema escuro com suporte a transparência (Glassmorphism).
- **SearchBar:** Barra de pesquisa integrada para filtrar funções automaticamente.
- **Save/Load System:** Salva e carrega configurações automaticamente usando Flags.
- **Animações Suaves:** Interações elásticas via TweenService.
- **Componentes Completos:**
  - Abas, Botões, Toggles, Sliders.
  - Dropdowns (Multi/Single), Color Pickers, TextBoxes.
- **Sistema de Notificações:** Toast notifications integradas.

## 📦 Instalação

Copie o código abaixo e cole no seu executor (Script):

```lua
local Library = loadstring(game:HttpGet("LINK_DO_SEU_RAW_AQUI"))()
```

> ⚠️ **Nota:** Substitua `"LINK_DO_SEU_RAW_AQUI"` pelo link **Raw** do arquivo `.lua` que você subiu no seu repositório.

---

## 🚀 Documentação

### 1. Carregar Configuração (Opcional)
Se você quiser que o script lembre as configurações ao iniciar, adicione esta linha **antes** de criar a janela. O sistema verificará se a pasta e o arquivo existem.

```lua
-- Carrega a config "MinhaConfig" se ela existir
Library.Flags = Library:SafeLoad("MinhaConfig") or {}
```

### 2. Criar Janela
A função principal para iniciar a UI.

```lua
local Window = Library:CreateWindow({
    Title = "Hub Premium",
    Color = Color3.fromRGB(0, 255, 140), -- Cor de destaque
    MinimizeKey = Enum.KeyCode.RightControl, -- Tecla para minimizar
    Transparent = true, -- (Opcional) Fundo Transparente
    SearchBar = true    -- (Opcional) Ativa a barra de pesquisa no topo
})
```

### 3. Notificações
Envia um alerta no canto da tela.

```lua
-- Título, Texto, Duração
Library:Notify("Aviso", "Script carregado com sucesso!", 3)
```

---

## 🛠 Componentes & Flags

Para usar o sistema de **Save/Load**, você deve adicionar o parâmetro `Flag` nas configurações dos componentes. A Library usará esse ID para salvar ou carregar o valor.

### Abas (Tabs)
```lua
local Tab = Window:AddTab("Principal", "rbxassetid://123456789")
```

### Button
Botões não salvam estado, servem apenas para executar ações.
```lua
Tab:AddButton("Clique Aqui", function()
    print("Botão pressionado")
end)
```

### Toggle (Com Save)
```lua
Tab:AddToggle("Auto Farm", {
    Default = false,
    Flag = "AutoFarmKey" -- ID único para salvar
}, function(Value)
    print("Auto Farm está:", Value)
end)
```

### Slider (Com Save)
```lua
Tab:AddSlider("Velocidade", {
    Min = 16,
    Max = 100,
    Default = 16,
    Flag = "WalkSpeedKey" -- ID único
}, function(Value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
end)
```

### Dropdown (Com Save)
Suporta seleção única ou múltipla.

```lua
Tab:AddDropdown("Selecione a Arma", {
    Values = {"Rifle", "Pistola", "Faca"},
    Default = "Rifle",
    Multi = false,
    Flag = "WeaponSelector" -- ID único
}, function(Value)
    print("Selecionado:", Value)
end)
```

### Color Picker (Com Save)
```lua
Tab:AddColorPicker("Cor da ESP", Color3.fromRGB(255, 0, 0), {
    Flag = "EspColor" -- ID único
}, function(Color)
    print(Color.R, Color.G, Color.B)
end)
```

### TextBox (Com Save)
```lua
Tab:AddTextBox("Mensagem de Spam", {
    Flag = "SpamText"
}, function(Text)
    print("Texto salvo:", Text)
end)
```

---

## 💾 Salvando Configurações

Para que o usuário possa salvar as alterações feitas, você precisa criar um botão que chame a função `SafeSave`.

```lua
local SettingsTab = Window:AddTab("Configurações", "")

SettingsTab:AddButton("Salvar Config", function()
    Library:SafeSave("MinhaConfig") -- Cria o arquivo "MinhaConfig.json"
    Library:Notify("Config", "Salvo com sucesso!", 2)
end)

SettingsTab:AddButton("Deletar Config", function()
    delfile("MyDarkLib/MinhaConfig.json") -- Deleta o arquivo
    Library:Notify("Config", "Configuração deletada.", 2)
end)
```

---

## 📜 Exemplo de Script Completo

Aqui está um exemplo funcional juntando tudo:

```lua
local Library = loadstring(game:HttpGet("LINK_DO_SEU_RAW_AQUI"))()

-- 1. Carrega configurações salvas (se existirem)
Library.Flags = Library:SafeLoad("ConfigExample") or {}

-- 2. Cria a Janela
local Window = Library:CreateWindow({
    Title = "Script Hub V2",
    Color = Color3.fromRGB(255, 170, 0),
    Transparent = true,
    SearchBar = true
})

-- 3. Cria Abas e Funções
local Tab = Window:AddTab("Farm", "")

Tab:AddToggle("Auto Farm", {Default = false, Flag = "FarmEnabled"}, function(v)
    print("Farm:", v)
end)

Tab:AddSlider("Distância", {Min = 0, Max = 50, Default = 10, Flag = "FarmDist"}, function(v)
    print("Dist:", v)
end)

-- 4. Aba de Configurações
local ConfigTab = Window:AddTab("Sistema", "")

ConfigTab:AddButton("Salvar Tudo", function()
    Library:SafeSave("ConfigExample")
    Library:Notify("Sistema", "Configuração Salva!", 3)
end)
```

## 📝 Créditos

Desenvolvido por **[66six__]**.
