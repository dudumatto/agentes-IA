# upload-security

Checklist:
- validar tipo/tamanho (MIME + assinatura quando possível)
- path traversal: normalizar e garantir “dentro de uploads/”
- nomes únicos (não confiar no filename)
- headers de download seguros (`nosniff`, `Content-Disposition`)

