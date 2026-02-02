# 🎨 Modern UI Library V2

Uma biblioteca de interface (UI) para Roblox minimalista, moderna e totalmente animada. Desenvolvida em Luau com foco em UX (Experiência do Usuário), contando com animações suaves (TweenService) e suporte a temas transparentes.


## ✨ Funcionalidades

- **Design Premium:** Tema escuro com suporte a transparência (Glassmorphism).
- **Animações Suaves:** Interações elásticas, fade-ins e transições de abas.
- **Componentes Completos:**
  - Abas com ícones e barra lateral animada.
  - **Color Picker** (RGB) e **TextBox**.
  - Dropdowns com Multi-Seleção e Refresh.
  - Sliders, Toggles e Botões interativos.
- **Sistema de Notificações:** Toast notifications integradas.
- **Funcional:** Janela arrastável e minimizável (com tecla configurável).

## 📦 Instalação

Copie o código abaixo e cole no seu executor (Script):

```lua
local Library = loadstring(game:HttpGet("SEU_LINK_RAW_AQUI"))()

> ⚠️ Nota: Lembre-se de substituir "SEU_LINK_RAW_AQUI" pelo link Raw do arquivo .lua do seu repositório GitHub.
> 
🚀 Documentação
1. Criar Janela
A função principal para iniciar a UI.
local Window = Library:CreateWindow({
    Title = "Nome do Script",
    Color = Color3.fromRGB(0, 255, 140), -- Cor de destaque (Accent)
    MinimizeKey = Enum.KeyCode.RightControl, -- Tecla para minimizar a UI
    Transparent = true -- (Novo) Define se o fundo será semitransparente
})

2. Notificações
Envia um alerta animado no canto inferior direito da tela.
-- Título, Mensagem, Duração (segundos)
Library:Notify("Sucesso", "Configuração carregada!", 3)

3. Abas (Tabs)
Cria uma nova aba na janela. O ícone é opcional.
-- Nome, Icon ID (rbxassetid://...) ou deixe vazio ""
local Tab = Window:AddTab("Principal", "rbxassetid://123456789")

🛠 Componentes
Label
Texto simples para separar seções ou dar avisos.
Tab:AddLabel("Configurações de Combate")

Button
Botão clicável que executa uma função.
Tab:AddButton("Executar Script", function()
    print("Botão clicado!")
end)

Toggle
Interruptor On/Off.
Tab:AddToggle("Auto Farm", {Default = false}, function(Value)
    print("Estado:", Value) -- Retorna true ou false
end)

Slider
Barra deslizante para selecionar números.
Tab:AddSlider("Velocidade", {
    Min = 16,
    Max = 100,
    Default = 16
}, function(Value)
    print("Valor:", Value)
end)

TextBox (Novo)
Caixa de entrada de texto.
Tab:AddTextBox("Mensagem de Spam", function(Text)
    print("Você digitou:", Text)
end)

Color Picker (Novo)
Seletor de cores com sliders RGB.
Tab:AddColorPicker("Cor da ESP", Color3.fromRGB(255, 0, 0), function(Color)
    -- Retorna um Color3
    print(Color.R, Color.G, Color.B) 
end)

Dropdown
Lista de seleção. Suporta seleção única ou múltipla.
Modo Único:
local Drop = Tab:AddDropdown("Selecione Arma", {
    Values = {"M4A1", "AK-47", "Sniper"},
    Default = "M4A1",
    Multi = false
}, function(Value)
    print("Selecionado:", Value)
end)

Modo Múltiplo:
Tab:AddDropdown("Teleportes", {
    Values = {"Spawn", "Loja", "PvP"},
    Default = "",
    Multi = true
}, function(Options)
    -- Retorna uma tabela: {"Spawn" = true, "Loja" = false...}
    for Option, State in pairs(Options) do
        if State then print(Option .. " está ativado") end
    end
end)

Atualizar Lista (Refresh):
Você pode atualizar os itens de um dropdown existente:
Drop:Refresh({"Nova Lista 1", "Nova Lista 2"})

📜 Exemplo Completo
Aqui está um script de exemplo para testar todas as funções:
local Library = loadstring(game:HttpGet("SEU_LINK_RAW_AQUI"))()

local Window = Library:CreateWindow({
    Title = "Showcase UI",
    Color = Color3.fromRGB(255, 120, 0),
    Transparent = true
})

Library:Notify("Bem-vindo", "UI Carregada com sucesso!", 5)

local Tab = Window:AddTab("Main", "")

Tab:AddLabel("Teste de Componentes")

Tab:AddToggle("God Mode", {Default = false}, function(s)
    print(s)
end)

Tab:AddColorPicker("Cor do Menu", Color3.new(1,1,1), function(c)
    print(c)
end)

Tab:AddTextBox("Digite algo", function(t)
    print(t)
end)

📝 Créditos
Desenvolvido por [Seu Nome].

### O que você precisa fazer agora:
1.  Crie um arquivo chamado `README.md` no seu GitHub.
2.  Cole o código acima.
3.  **Importante:** Onde está escrito `SEU_LINK_RAW_AQUI`, o usuário final terá que colocar o link do seu script. Você pode já deixar o seu link fixo se quiser.
4.  Onde tem o link da imagem (`https://via.placeholder.com...`), substitua pelo link de uma print (screenshot) real da sua UI funcionando no jogo. Isso atrai muito mais downloads/uso!

