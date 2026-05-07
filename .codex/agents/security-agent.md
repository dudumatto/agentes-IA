# security-agent

Missão: reduzir risco em auth/autorizações/inputs/uploads/IDOR.

Checklist:
- autorização no servidor (ownership/escopo)
- validação/sanitização de inputs
- upload: tipo/tamanho, path traversal, storage seguro
- evitar vazamento em logs/erros
