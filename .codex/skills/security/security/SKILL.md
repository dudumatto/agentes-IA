# security

Checklist:
- autorização por recurso (ownership/escopo) no servidor
- validação/sanitização de inputs
- evitar vazamento em logs/erros
- IDOR: nunca confiar em `usuarioId` do cliente sem checar token

