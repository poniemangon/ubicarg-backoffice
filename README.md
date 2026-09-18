# UbicaRG Admin

Panel de administración de [UbicaRG](https://github.com/poniemangon/ubicarg) — copia de [UbiCABA Admin](https://github.com/poniemangon/ubicaba-admin) adaptada a la escala país: localidades en vez de esquinas, provincias en vez de barrios.

## Desarrollo local

```bash
npm install
npm run dev
```

Necesita un `.env` con:

```
VITE_SUPABASE_URL=...
VITE_SUPABASE_PUBLISHABLE_KEY=...
```

(las mismas que usa el proyecto de ubicarg — comparten la misma base de Supabase).

## Volverse admin

El login es Supabase Auth nativo (email/contraseña), sin registro público. Para poder entrar:

1. Creá el usuario en Supabase Dashboard → Authentication → Users → Add user (o registrate como jugador normal desde la app principal de ubicarg).
2. Necesitás también una fila en `profiles` con `is_admin = true` — si te registraste desde la app principal ya tenés la fila `profiles`, así que solo hace falta:
   ```sql
   update profiles set is_admin = true where username = '<tu usuario>';
   ```

## Storage

Usa dos buckets públicos de Supabase Storage: `admin-uploads` (imágenes genéricas — popups, etc.) y `localidad-images` (fotos por localidad). Ver `supabase/migrations/0006_storage_buckets_rls.sql` en el repo de ubicarg para las policies de escritura.
