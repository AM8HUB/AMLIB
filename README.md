# 🎨 Am lib

Uma biblioteca de interface gráfica (UI) moderna, minimalista e altamente configurável para scripts de Roblox (Luau). Possui suporte a temas escuros, animações suaves, **barra de pesquisa integrada** e sistema de notificações.

## ✨ Funcionalidades

- **Design Clean:** Tema escuro agradável com cores de destaque personalizáveis.
- **Search Bar:** Barra de pesquisa funcional que filtra e encontra elementos em qualquer aba.
- **Componentes:** Suporte a Toggles, Sliders, Dropdowns (Multi/Single), Color Pickers e TextBoxes.
- **Draggable:** Janela principal e botão de abrir flutuante móveis.
- **Notificações:** Sistema de avisos toast embutido.

## 📦 Como Usar

### Inicialização
Para carregar a library, utilize o `loadstring` (se estiver em um executor).

```lua
local Library = loadstring(game:HttpGet("LINK PRIVADO"))()
```

## 🛠️ Documentação

### 1. Criar Janela
A janela principal é o container do seu hub.

```lua
local Window = Library:CreateWindow({
    Title = "Hub Title",                  -- Nome da Janela
    Color = Color3.fromRGB(0, 255, 140),  -- Cor de destaque (Accent)
    MinimizeKey = Enum.KeyCode.RightControl, -- Tecla para minimizar
    Transparent = true,                   -- Fundo transparente (true/false)
    SearchBar = true                      -- Ativa a barra de busca (true/false)
})
```

### 2. Criar Abas
Organize seus scripts em categorias. Você pode usar IDs de imagem do Roblox para ícones.

```lua
local MainTab = Window:AddTab("Principal", "6034509993")
local VisualsTab = Window:AddTab("Visuais", "6031763426")
```

---

### 🧩 Elementos da UI

#### Label (Texto)
Adiciona um texto informativo. Retorna uma função `.Set()` para atualizar o texto depois.
```lua
local StatusLabel = MainTab:AddLabel("Status: Aguardando...")

-- Atualizar texto:
StatusLabel:Set("Status: Ativado!")
```

#### Button (Botão)
Executa uma ação ao ser clicado.
```lua
MainTab:AddButton("Resetar Personagem", function()
    game.Players.LocalPlayer.Character:BreakJoints()
end)
```

#### Toggle (Interruptor)
Botão de ON/OFF. Útil para loops.
```lua
MainTab:AddToggle("Auto Farm", {Default = false}, function(State)
    -- 'State' retorna true ou false
    if State then
        print("Farm ligado")
    else
        print("Farm desligado")
    end
end)
```

#### Slider (Barra Deslizante)
Para selecionar números dentro de um intervalo.
```lua
MainTab:AddSlider("Velocidade", {
    Min = 16,
    Max = 200,
    Default = 16
}, function(Value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
end)
```

#### TextBox (Caixa de Texto)
Campo para o usuário digitar. O callback é acionado quando o usuário tira o foco da caixa (Enter ou Clicar fora).
```lua
MainTab:AddTextBox("Nome do Alvo", function(Text)
    print("Texto digitado: " .. Text)
end)
```

#### Color Picker (Seletor de Cor)
Permite escolher uma cor RGB.
```lua
VisualsTab:AddColorPicker("Cor da ESP", Color3.fromRGB(255, 255, 255), function(Color)
    -- 'Color' é um Color3
    print("Nova cor:", Color)
end)
```

#### Dropdown (Lista de Seleção)
Suporta seleção única ou múltipla.

**Modo Único (Single):**
```lua
MainTab:AddDropdown("Escolha o Time", {
    Values = {"Red", "Blue", "Green"},
    Default = "Red",
    Multi = false
}, function(Value)
    -- Retorna a string selecionada
    print("Time:", Value)
end)
```

**Modo Múltiplo (Multi):**
```lua
MainTab:AddDropdown("Selecionar Itens", {
    Values = {"Espada", "Escudo", "Poção"},
    Default = "",
    Multi = true
}, function(Table)
    -- Retorna uma tabela: { ["Espada"] = true, ["Poção"] = false }
    for item, ativo in pairs(Table) do
        if ativo then print(item .. " selecionado") end
    end
end)
```

---

### 🔔 Notificações
Envia um alerta toast no canto da tela.

```lua
-- Library:Notify(Título, Texto, Duração)
Library:Notify("Sucesso", "Configuração salva!", 5)
```

## 📝 Exemplo Completo

Aqui está um script completo pronto para teste:

```lua
local Library = require(script.Library) -- Ajuste o caminho

local Window = Library:CreateWindow({
    Title = "Super Hub v2",
    Color = Color3.fromRGB(255, 170, 0),
    MinimizeKey = Enum.KeyCode.LeftAlt,
    SearchBar = true
})

local Tab1 = Window:AddTab("Jogados")
local Tab2 = Window:AddTab("Config")

Tab1:AddToggle("God Mode", {Default = false}, function(v)
    print("God Mode:", v)
end)

Tab1:AddSlider("Pulo", {Min = 50, Max = 500}, function(v)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = v
end)

Tab2:AddButton("Fechar UI", function()
    game.CoreGui:FindFirstChild("MyDarkLib"):Destroy()
end)

Library:Notify("Bem-vindo", "Script carregado com sucesso!", 3)
```
