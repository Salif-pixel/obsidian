
---
📁 src/
  ├─ app/
  │  ├─ (public)/                      # Routes publiques
  │  │  ├─ page.tsx                    # Page d'accueil
  │  │  ├─ login/                      # Authentification
  │  │  │  └─ page.tsx
  │  │  └─ register/                   # Inscription
  │  │     └─ page.tsx
  │  │
  │  ├─ (protected)/                   # Routes protégées
  │  │  ├─ layout.tsx                  # Layout authentifié
  │  │  │
  │  │  ├─ professor/                  # Espace professeur
  │  │  │  ├─ layout.tsx
  │  │  │  ├─ page.tsx                # Dashboard prof
  │  │  │  │
  │  │  │  ├─ @sidebar/               # Parallel: Menu dynamique
  │  │  │  │  ├─ default.tsx
  │  │  │  │  └─ loading.tsx
  │  │  │  │
  │  │  │  ├─ documents/              # Gestion documents
  │  │  │  │  ├─ page.tsx            # Liste documents
  │  │  │  │  ├─ loading.tsx
  │  │  │  │  ├─ error.tsx
  │  │  │  │  │
  │  │  │  │  ├─ @preview/           # Parallel: Prévisualisation
  │  │  │  │  │  ├─ default.tsx
  │  │  │  │  │  └─ loading.tsx
  │  │  │  │  │
  │  │  │  │  ├─ create/            # Création document
  │  │  │  │  │  └─ page.tsx
  │  │  │  │  │
  │  │  │  │  └─ [id]/              # Détail document
  │  │  │  │     ├─ page.tsx
  │  │  │  │     └─ edit/
  │  │  │  │        └─ page.tsx
  │  │  │  │
  │  │  │  ├─ exams/                # Gestion examens
  │  │  │  │  ├─ page.tsx          # Liste examens
  │  │  │  │  ├─ loading.tsx
  │  │  │  │  ├─ error.tsx
  │  │  │  │  │
  │  │  │  │  ├─ @active/          # Parallel: Examens actifs
  │  │  │  │  │  ├─ default.tsx
  │  │  │  │  │  └─ loading.tsx
  │  │  │  │  │
  │  │  │  │  ├─ @stats/           # Parallel: Stats live
  │  │  │  │  │  ├─ default.tsx
  │  │  │  │  │  └─ loading.tsx
  │  │  │  │  │
  │  │  │  │  ├─ create/           # Création examen
  │  │  │  │  │  └─ page.tsx
  │  │  │  │  │
  │  │  │  │  └─ [id]/             # Détail examen
  │  │  │  │     ├─ page.tsx
  │  │  │  │     ├─ edit/
  │  │  │  │     │  └─ page.tsx
  │  │  │  │     │
  │  │  │  │     ├─ @submissions/  # Parallel: Soumissions
  │  │  │  │     │  ├─ default.tsx
  │  │  │  │     │  └─ loading.tsx
  │  │  │  │     │
  │  │  │  │     └─ @results/      # Parallel: Résultats
  │  │  │  │        ├─ default.tsx
  │  │  │  │        └─ loading.tsx
  │  │  │  │
  │  │  │  └─ analytics/           # Analytics
  │  │  │     ├─ page.tsx
  │  │  │     └─ loading.tsx
  │  │  │
  │  │  └─ student/                # Espace étudiant
  │  │     ├─ layout.tsx
  │  │     ├─ page.tsx            # Dashboard étudiant
  │  │     │
  │  │     ├─ @notifications/     # Parallel: Notifications
  │  │     │  ├─ default.tsx
  │  │     │  └─ loading.tsx
  │  │     │
  │  │     ├─ exams/              # Examens étudiant
  │  │     │  ├─ page.tsx        # Liste examens
  │  │     │  │
  │  │     │  ├─ @upcoming/      # Parallel: Prochains examens
  │  │     │  │  ├─ default.tsx
  │  │     │  │  └─ loading.tsx
  │  │     │  │
  │  │     │  └─ [id]/           # Détail/passage examen
  │  │     │     ├─ page.tsx
  │  │     │     ├─ take/        # Passage examen
  │  │     │     │  └─ page.tsx
  │  │     │     │
  │  │     │     ├─ @timer/      # Parallel: Timer examen
  │  │     │     │  ├─ default.tsx
  │  │     │     │  └─ loading.tsx
  │  │     │     │
  │  │     │     └─ @progress/   # Parallel: Progression
  │  │     │        ├─ default.tsx
  │  │     │        └─ loading.tsx
  │  │     │
  │  │     └─ results/           # Résultats étudiant
  │  │        └─ page.tsx
  │  │
  │  └─ api/                     # Routes API
  │     ├─ auth/
  │     │  └─ [...nextauth]/
  │     │     └─ route.ts
  │     │
  │     ├─ documents/
  │     │  ├─ route.ts
  │     │  └─ [id]/
  │     │     └─ route.ts
  │     │
  │     └─ exams/
  │        ├─ route.ts
  │        └─ [id]/
  │           └─ route.ts
  │
  ├─ lib/
  │  ├─ actions/                 # Server Actions
  │  │  ├─ auth.ts
  │  │  ├─ documents.ts
  │  │  ├─ exams.ts
  │  │  └─ results.ts
  │  │
  │  ├─ api/                    # Clients API externes
  │  │  ├─ flask.ts
  │  │  └─ types.ts
  │  │
  │  ├─ auth/                   # Auth utils
  │  │  ├─ config.ts
  │  │  └─ utils.ts
  │  │
  │  ├─ db/                     # Database
  │  │  ├─ index.ts
  │  │  └─ schema.ts
  │  │
  │  └─ utils/                  # Utilitaires
  │     ├─ constants.ts
  │     └─ helpers.ts
  │
  ├─ components/
  │  ├─ auth/                   # Composants auth
  │  │  ├─ login-form.tsx
  │  │  └─ register-form.tsx
  │  │
  │  ├─ documents/             # Composants documents
  │  │  ├─ document-card.tsx
  │  │  └─ document-form.tsx
  │  │
  │  ├─ exams/                # Composants examens
  │  │  ├─ exam-card.tsx
  │  │  └─ exam-form.tsx
  │  │
  │  ├─ ui/                   # Composants UI
  │  │  ├─ button.tsx
  │  │  ├─ input.tsx
  │  │  └─ card.tsx
  │  │
  │  └─ shared/               # Composants partagés
  │     ├─ header.tsx
  │     └─ footer.tsx
  │
  ├─ hooks/                   # Custom hooks
  │  ├─ use-auth.ts
  │  └─ use-exam.ts
  │
  ├─ styles/                  # Styles
  │  └─ globals.css
  │
  └─ types/                   # Types TypeScript
     ├─ auth.ts
     ├─ document.ts
     └─ exam.ts

📁 prisma/                    # Prisma
  ├─ migrations/
  └─ schema.prisma

📁 public/                    # Assets statiques
  ├─ images/
  └─ icons/

📁 flask_api/                 # API Flask
  ├─ app/
  │  ├─ __init__.py
  │  ├─ routes/
  │  ├─ models/
  │  └─ services/
  │
  ├─ config.py
  ├─ requirements.txt
  └─ wsgi.py