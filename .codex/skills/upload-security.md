# upload-security

- Validar tipo/tamanho (MIME + assinatura quando possível).
- Bloquear path traversal; garantir caminho “dentro de uploads/”.
- Nomear/armazenar com IDs (não confiar em filename).
- Download seguro: `Content-Disposition`, `nosniff`, content-type correto.

