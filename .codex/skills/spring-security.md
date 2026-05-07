# spring-security

- Autorização por recurso (ownership/escopo) no servidor.
- Não confiar em `usuarioId` do cliente sem checar token/role.
- Evitar IDOR: validar que o recurso pertence ao usuário.
- Tratar 401/403 de forma consistente e testável.

