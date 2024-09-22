 DEUXE MEU CREDITOSNA CRIAÇÃO DO SISTEMA
BY ALBINO MODS










const fs = require("fs-extra");
const path = "./database/usuariosSystemRPG";

// Função para ler o arquivo de usuários
const lerUsuarios = () => {
    try {
        return JSON.parse(fs.readFileSync(path));
    } catch (error) {
        console.error("Erro ao ler o arquivo:", error);
        return [];
    }
};

// Função para salvar o arquivo de usuários
const salvarUsuarios = (usuarios) => {
    try {
        fs.writeFileSync(path, JSON.stringify(usuarios, null, 2));
    } catch (error) {
        console.error("Erro ao salvar o arquivo:", error);
    }
};

// Função para adicionar ryò
exports.AdicionarRyò = (UserID, ValorA) => {
    const usuarios = lerUsuarios();
    const user = usuarios.find(i => i.id === UserID);

    if (user) {
        user.ryò = (user.ryò || 0) + Number(ValorA);
        salvarUsuarios(usuarios);
    } else {
        console.error("Usuário não encontrado:", UserID);
    }
};

// Função para remover ryò
exports.RemoverRyò = (UserID, ValorR) => {
    const usuarios = lerUsuarios();
    const user = usuarios.find(i => i.id === UserID);

    if (user) {
        user.ryò = (user.ryò || 0) - Number(ValorR);
        salvarUsuarios(usuarios);
    } else {
        console.error("Usuário não encontrado:", UserID);
    }
};

// Função para verificar o saldo de ryò
exports.VerificarRyò = (UserID) => {
    const usuarios = lerUsuarios();
    const user = usuarios.find(i => i.id === UserID);

    if (user) {
        return user.ryò || 0;
    } else {
        console.error("Usuário não encontrado:", UserID);
        return null;
    }
};
