🚀 CONFIGURAÇÃO COMPLETA PARA ESTRUTURA lpremaviva/frontend

ESTRUTURA ATUAL
text
lpremaviva/
├── frontend/   ← VAMOS TRABALHAR AQUI
└── backend/    ← Para depois

# 0. ENTRAR NA PASTA E CRIAR PACKAGE.JSON
bash
# 1. Navegar para a pasta frontend
cd lpremaviva/frontend

# 2. Criar package.json manualmente (ou usar npm init)
npm init -y

# 3. Editar o package.json criado

# 2. CONFIGURAR PACKAGE.JSON COMPLETO
Edite o package.json para ficar assim:

json
{
  "name": "lpremaviva-frontend",
  "version": "0.1.0",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "format": "prettier --write \"src/**/*.{ts,tsx,js,jsx,css,json}\"",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "lucide-react": "^0.309.0",
    "axios": "^1.6.0",
    "react-hot-toast": "^2.4.1"
  },
  "devDependencies": {
    "@types/react": "^18.2.43",
    "@types/react-dom": "^18.2.17",
    "@typescript-eslint/eslint-plugin": "^6.14.0",
    "@typescript-eslint/parser": "^6.14.0",
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.16",
    "eslint": "^8.55.0",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.5",
    "postcss": "^8.4.32",
    "tailwindcss": "^3.4.0",
    "typescript": "^5.2.2",
    "vite": "^5.0.8",
    "prettier": "^3.1.1"
  },
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=8.0.0"
  }
}

3. INSTALAR DEPENDÊNCIAS
bash
# Instalar tudo de uma vez
npm install

# OU se preferir instalar passo a passo:
npm install react react-dom
npm install lucide-react axios react-hot-toast
npm install -D typescript @types/react @types/react-dom
npm install -D vite @vitejs/plugin-react
npm install -D tailwindcss postcss autoprefixer
npm install -D eslint prettier

4. CRIAR ARQUIVOS DE CONFIGURAÇÃO
4.1 TypeScript Config
Crie tsconfig.json:

json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": false,
    "noUnusedParameters": false,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"],
      "@hooks/*": ["src/hooks/*"]
    }
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
Crie tsconfig.node.json:

json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true,
    "strict": true
  },
  "include": ["vite.config.ts"]
}
4.2 Vite Config
Crie vite.config.ts:

typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
      '@components': path.resolve(__dirname, './src/components'),
      '@utils': path.resolve(__dirname, './src/utils'),
      '@hooks': path.resolve(__dirname, './src/hooks'),
    }
  },
  server: {
    port: 5173,
    host: true,
    open: true
  },
  build: {
    outDir: 'dist',
    sourcemap: false,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          ui: ['lucide-react']
        }
      }
    }
  }
})
4.3 Tailwind CSS Config
Crie tailwind.config.js:

javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
        },
        secondary: {
          50: '#f0fdf4',
          100: '#dcfce7',
          200: '#bbf7d0',
          300: '#86efac',
          400: '#4ade80',
          500: '#22c55e',
          600: '#16a34a',
          700: '#15803d',
          800: '#166534',
          900: '#14532d',
        },
        accent: {
          50: '#fefce8',
          100: '#fef9c3',
          200: '#fef08a',
          300: '#fde047',
          400: '#facc15',
          500: '#eab308',
          600: '#ca8a04',
          700: '#a16207',
          800: '#854d0e',
          900: '#713f12',
        }
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
      animation: {
        'fade-in': 'fadeIn 0.5s ease-in-out',
        'slide-up': 'slideUp 0.3s ease-out',
        'pulse-slow': 'pulse 3s ease-in-out infinite',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' }
        },
        slideUp: {
          '0%': { transform: 'translateY(10px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' }
        }
      }
    },
  },
  plugins: [],
}
Crie postcss.config.js:

javascript
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
4.4 ESLint Config (opcional mas recomendado)
Crie .eslintrc.cjs:

javascript
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react-hooks/recommended',
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parser: '@typescript-eslint/parser',
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
    '@typescript-eslint/no-unused-vars': 'warn',
    '@typescript-eslint/no-explicit-any': 'warn',
  },
}
5. CRIAR ESTRUTURA DE PASTAS E ARQUIVOS PRINCIPAIS
5.1 Criar estrutura de pastas
bash
mkdir -p src/components/ui
mkdir -p src/components/sections
mkdir -p src/hooks
mkdir -p src/utils
mkdir -p src/services
mkdir -p src/types
mkdir -p src/assets
mkdir public
5.2 Criar arquivos HTML e CSS
Crie index.html:

html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Editora Rema Viva | Material de Catequese Calvinista</title>
    <meta name="description" content="Material cristocêntrico e fiel à teologia calvinista para pais, professores e líderes de ministério infantil.">
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    
    <!-- Meta tags para SEO e redes sociais -->
    <meta property="og:title" content="Editora Rema Viva">
    <meta property="og:description" content="Material cristocêntrico e fiel à teologia calvinista">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://editoraremaviva.com">
    <meta property="og:image" content="https://editoraremaviva.com/og-image.jpg">
    
    <!-- Favicon -->
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
    <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
    <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
    <link rel="manifest" href="/site.webmanifest">
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
Crie src/index.css:

css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  html {
    scroll-behavior: smooth;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    @apply font-sans text-gray-800 bg-white;
  }

  h1, h2, h3, h4, h5, h6 {
    @apply font-bold tracking-tight;
  }
}

@layer components {
  .btn-primary {
    @apply inline-flex items-center justify-center gap-2 px-6 py-3 text-base font-semibold text-white transition-all duration-300 bg-gradient-to-r from-primary-600 to-secondary-600 rounded-lg hover:from-primary-700 hover:to-secondary-700 hover:shadow-lg hover:scale-105 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed;
  }

  .btn-secondary {
    @apply inline-flex items-center justify-center gap-2 px-6 py-3 text-base font-semibold transition-all duration-300 bg-accent-400 text-primary-900 rounded-lg hover:bg-accent-300 hover:shadow-lg focus:outline-none focus:ring-2 focus:ring-accent-500 focus:ring-offset-2;
  }

  .btn-outline {
    @apply inline-flex items-center justify-center gap-2 px-6 py-3 text-base font-semibold transition-all duration-300 border-2 border-primary-600 text-primary-600 rounded-lg hover:bg-primary-50 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2;
  }

  .card {
    @apply bg-white rounded-xl shadow-lg border border-gray-100 p-6 transition-all duration-300 hover:shadow-xl;
  }

  .input-field {
    @apply w-full px-4 py-3 text-gray-700 bg-white border border-gray-300 rounded-lg focus:border-primary-500 focus:ring-2 focus:ring-primary-200 focus:outline-none transition-colors;
  }

  .section-container {
    @apply max-w-7xl mx-auto px-4 sm:px-6 lg:px-8;
  }

  .section-padding {
    @apply py-12 sm:py-16 lg:py-20;
  }

  .gradient-text {
    @apply bg-gradient-to-r from-primary-600 to-secondary-600 bg-clip-text text-transparent;
  }
}

/* Animations personalizadas */
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}
5.3 Criar arquivos TypeScript principais
Crie src/main.tsx:

tsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Toaster } from 'react-hot-toast'
import App from './App'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
    <Toaster 
      position="top-right"
      toastOptions={{
        duration: 4000,
        style: {
          background: '#1e3a8a',
          color: '#fff',
          borderRadius: '8px',
          padding: '16px',
        },
        success: {
          duration: 3000,
          iconTheme: {
            primary: '#22c55e',
            secondary: '#fff',
          },
        },
        error: {
          duration: 4000,
          iconTheme: {
            primary: '#ef4444',
            secondary: '#fff',
          },
        },
      }}
    />
  </React.StrictMode>
)
5.4 Criar arquivos de tipos e constantes
Crie src/types/index.ts:

typescript
export interface FormData {
  nome: string;
  email: string;
  whatsapp: string;
}

export interface Testimonial {
  id: number;
  name: string;
  role: string;
  text: string;
  rating: number;
}

export interface FAQ {
  id: number;
  question: string;
  answer: string;
}

export interface Plan {
  id: 'monthly' | 'yearly';
  name: string;
  price: number;
  originalPrice?: number;
  discount?: number;
  period: string;
  features: string[];
  ctaText: string;
  highlighted?: boolean;
}

export interface CountdownTime {
  hours: number;
  minutes: number;
  seconds: number;
}
Crie src/utils/constants.ts:

typescript
export const COUNTDOWN_INITIAL = {
  hours: 23,
  minutes: 45,
  seconds: 30
} as const;

export const TESTIMONIALS = [
  {
    id: 1,
    name: 'Rev. João Silva',
    role: 'Pastor, Igreja Presbiteriana',
    text: 'Material de excelente qualidade teológica. Nossos professores economizam horas de preparação e as crianças estão aprendendo com profundidade.',
    rating: 5
  },
  {
    id: 2,
    name: 'Ana Paula',
    role: 'Professora Escola Dominical',
    text: 'Finalmente encontrei material que é fiel à doutrina reformada e ainda assim acessível para as crianças. As atividades são incríveis!',
    rating: 5
  },
  {
    id: 3,
    name: 'Marcos Costa',
    role: 'Líder Ministério Infantil',
    text: 'A abordagem cristocêntrica é exatamente o que precisávamos. As crianças estão engajadas e os pais elogiando o conteúdo.',
    rating: 5
  }
] as const;

export const FAQS = [
  {
    id: 1,
    question: 'O conteúdo é mesmo fiel à teologia reformada?',
    answer: 'Sim! Todo o material é desenvolvido com base nas Escrituras e alinhado com a Confissão de Fé de Westminster e os Catecismos. Nosso compromisso é com a fidelidade bíblica e doutrinária.'
  },
  {
    id: 2,
    question: 'Com que frequência recebo novos materiais?',
    answer: 'Os assinantes recebem lições semanais completas, totalizando 4 lições por mês. Além disso, disponibilizamos materiais especiais para datas comemorativas.'
  },
  {
    id: 3,
    question: 'Posso cancelar a assinatura quando quiser?',
    answer: 'Sim! Não há fidelidade. Você pode cancelar a qualquer momento sem custos adicionais. No plano mensal, o cancelamento vale a partir do próximo mês.'
  },
  {
    id: 4,
    question: 'Os materiais são para qual faixa etária?',
    answer: 'Oferecemos conteúdo segmentado por faixas etárias: Maternal (3-6 anos), Júnior (7-10 anos) e Adolescentes (11-14 anos), com abordagens pedagógicas adequadas.'
  },
  {
    id: 5,
    question: 'Como acesso os materiais após a assinatura?',
    answer: 'Imediatamente após a confirmação do pagamento, você recebe acesso à área de membros com todos os PDFs disponíveis para download e impressão.'
  },
  {
    id: 6,
    question: 'Posso usar os materiais na minha igreja?',
    answer: 'Sim! Os materiais podem ser usados livremente em igrejas, escolas bíblicas e ministérios cristãos. Você pode imprimir quantas cópias precisar para seu ministério.'
  }
] as const;

export const PLANS = [
  {
    id: 'monthly' as const,
    name: 'Plano Mensal',
    price: 47,
    period: '/mês',
    features: [
      'Lições semanais completas',
      'Atividades prontas para imprimir',
      'Guias para professores',
      'Materiais visuais em PDF',
      'Acesso imediato ao conteúdo',
      'Cancele quando quiser'
    ],
    ctaText: 'Assinar Plano Mensal'
  },
  {
    id: 'yearly' as const,
    name: 'Plano Anual',
    price: 397,
    originalPrice: 564,
    discount: 30,
    period: '/ano',
    features: [
      'TUDO do Plano Mensal',
      '✨ 3 meses grátis',
      '🎁 Bônus exclusivos',
      '📚 E-books extras',
      '🎯 Acesso prioritário a novos materiais',
      '💎 Materiais especiais de datas comemorativas'
    ],
    ctaText: 'Assinar Plano Anual (Melhor Preço)',
    highlighted: true
  }
] as const;

export const GOOGLE_FORM_CONFIG = {
  url: 'https://docs.google.com/forms/u/0/d/e/FORM_ID/formResponse',
  fieldIds: {
    nome: 'entry.1234567890',
    email: 'entry.0987654321',
    whatsapp: 'entry.1357924680'
  }
} as const;

export const CONTACT_INFO = {
  email: 'contato@editoraremaviva.com.br',
  phone: '(14) 99999-9999',
  instagram: 'https://www.instagram.com/editoraremaviva/',
  whatsapp: 'https://wa.me/5514999999999'
} as const;
5.5 Criar hooks personalizados
Crie src/hooks/useCountdown.ts:

typescript
import { useState, useEffect } from 'react';
import { CountdownTime } from '@/types';

export const useCountdown = (initialTime: CountdownTime) => {
  const [timeLeft, setTimeLeft] = useState<CountdownTime>(initialTime);
  const [isActive, setIsActive] = useState(true);

  useEffect(() => {
    if (!isActive) return;

    const timer = setInterval(() => {
      setTimeLeft(prev => {
        if (prev.seconds > 0) {
          return { ...prev, seconds: prev.seconds - 1 };
        }
        if (prev.minutes > 0) {
          return { ...prev, minutes: prev.minutes - 1, seconds: 59 };
        }
        if (prev.hours > 0) {
          return { hours: prev.hours - 1, minutes: 59, seconds: 59 };
        }
        
        // Quando chegar a zero, para o timer
        setIsActive(false);
        return { hours: 0, minutes: 0, seconds: 0 };
      });
    }, 1000);

    return () => clearInterval(timer);
  }, [isActive]);

  const reset = () => {
    setTimeLeft(initialTime);
    setIsActive(true);
  };

  const pause = () => setIsActive(false);
  const resume = () => setIsActive(true);

  return {
    timeLeft,
    isActive,
    reset,
    pause,
    resume,
    formatted: {
      hours: String(timeLeft.hours).padStart(2, '0'),
      minutes: String(timeLeft.minutes).padStart(2, '0'),
      seconds: String(timeLeft.seconds).padStart(2, '0')
    }
  };
};
Crie src/hooks/useForm.ts:

typescript
import { useState, ChangeEvent, FormEvent } from 'react';

interface UseFormProps<T> {
  initialValues: T;
  onSubmit: (values: T) => Promise<void> | void;
  validate?: (values: T) => Partial<Record<keyof T, string>>;
}

export const useForm = <T extends Record<string, any>>({
  initialValues,
  onSubmit,
  validate
}: UseFormProps<T>) => {
  const [values, setValues] = useState<T>(initialValues);
  const [errors, setErrors] = useState<Partial<Record<keyof T, string>>>({});
  const [isSubmitting, setIsSubmitting] = useState(false);

  const handleChange = (e: ChangeEvent<HTMLInputElement | HTMLTextAreaElement>) => {
    const { name, value } = e.target;
    setValues(prev => ({
      ...prev,
      [name]: value
    }));

    // Limpa erro do campo quando usuário começa a digitar
    if (errors[name as keyof T]) {
      setErrors(prev => ({
        ...prev,
        [name]: undefined
      }));
    }
  };

  const handleSubmit = async (e: FormEvent) => {
    e.preventDefault();
    
    // Validação
    if (validate) {
      const validationErrors = validate(values);
      if (Object.keys(validationErrors).length > 0) {
        setErrors(validationErrors);
        return;
      }
    }

    try {
      setIsSubmitting(true);
      await onSubmit(values);
      // Limpa formulário após submit bem-sucedido
      setValues(initialValues);
    } catch (error) {
      console.error('Erro no formulário:', error);
    } finally {
      setIsSubmitting(false);
    }
  };

  const reset = () => {
    setValues(initialValues);
    setErrors({});
    setIsSubmitting(false);
  };

  return {
    values,
    errors,
    isSubmitting,
    handleChange,
    handleSubmit,
    reset,
    setValues
  };
};
6. AGORA VAMOS CRIAR O App.tsx COM SEU CÓDIGO
Crie src/App.tsx com este conteúdo INICIAL (depois você substitui pelo seu código completo):

tsx
import React, { useState } from 'react';
import { 
  Heart, BookOpen, Users, Download, Check, Star, Clock, 
  Shield, Mail, Phone, ChevronDown, Sparkles, Award, Book
} from 'lucide-react';
import { useCountdown } from '@/hooks/useCountdown';
import { useForm } from '@/hooks/useForm';
import { 
  COUNTDOWN_INITIAL, 
  TESTIMONIALS, 
  FAQS, 
  PLANS,
  CONTACT_INFO 
} from '@/utils/constants';
import { FormData } from '@/types';
import toast from 'react-hot-toast';

export default function App() {
  const { timeLeft, formatted } = useCountdown(COUNTDOWN_INITIAL);
  const [showFreeModal, setShowFreeModal] = useState(false);
  const [openFaqs, setOpenFaqs] = useState<number[]>([]);

  const form = useForm<FormData>({
    initialValues: {
      nome: '',
      email: '',
      whatsapp: ''
    },
    onSubmit: async (values) => {
      console.log('Enviando formulário:', values);
      toast.success('🎉 Obrigado! Verifique seu e-mail para baixar a lição gratuita.');
      setShowFreeModal(false);
    },
    validate: (values) => {
      const errors: Partial<Record<keyof FormData, string>> = {};
      if (!values.nome.trim()) errors.nome = 'Nome é obrigatório';
      if (!values.email.trim()) errors.email = 'E-mail é obrigatório';
      else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(values.email)) {
        errors.email = 'E-mail inválido';
      }
      return errors;
    }
  });

  const toggleFaq = (id: number) => {
    setOpenFaqs(prev => 
      prev.includes(id) 
        ? prev.filter(faqId => faqId !== id)
        : [...prev, id]
    );
  };

  const handleMonthlySubscription = () => {
    toast.loading('Redirecionando para pagamento...');
    // Aqui vai a integração com Pagar.me
    setTimeout(() => {
      toast.dismiss();
      toast.success('Redirecionando para checkout!');
      // window.location.href = checkoutUrl;
    }, 1500);
  };

  const handleYearlySubscription = () => {
    toast.loading('Redirecionando para pagamento...');
    // Aqui vai a integração com Pagar.me
    setTimeout(() => {
      toast.dismiss();
      toast.success('Redirecionando para checkout!');
      // window.location.href = checkoutUrl;
    }, 1500);
  };

  return (
    <div className="min-h-screen bg-gradient-to-b from-primary-50 to-white">
      {/* Hero Section */}
      <header className="relative overflow-hidden bg-gradient-to-r from-primary-600 via-primary-700 to-secondary-600 text-white">
        <div className="absolute inset-0 bg-black/10" />
        <div className="relative section-container section-padding">
          <div className="grid lg:grid-cols-2 gap-12 items-center">
            <div className="space-y-6">
              <div className="inline-flex items-center gap-2 bg-accent-400/20 backdrop-blur-sm text-accent-300 px-4 py-2 rounded-full text-sm font-semibold">
                <Sparkles className="w-4 h-4" />
                Material Cristocêntrico e Fiel à Doutrina Reformada
              </div>
              
              <h1 className="text-4xl md:text-5xl lg:text-6xl font-bold leading-tight">
                Transforme a Fé dos Seus Filhos com Lições Bíblicas{' '}
                <span className="text-accent-300">Inesquecíveis</span>
              </h1>
              
              <p className="text-xl text-primary-100">
                Conteúdo cristocêntrico e fiel à teologia calvinista, pronto para usar. 
                Economize horas de preparação e ministre com excelência.
              </p>
              
              <div className="flex flex-col sm:flex-row gap-4 pt-4">
                <button 
                  onClick={() => setShowFreeModal(true)}
                  className="btn-secondary text-lg px-8 py-4"
                >
                  <Download className="w-5 h-5" />
                  Baixe a Lição Gratuita Agora!
                </button>
                
                <a 
                  href="#planos" 
                  className="btn-outline text-lg px-8 py-4 text-white border-white hover:bg-white/10"
                >
                  <Book className="w-5 h-5" />
                  Ver Planos
                </a>
              </div>
              
              <p className="text-sm text-primary-200">
                🎁 Sem compromisso • Acesso imediato • 100% gratuito
              </p>
            </div>
            
            <div className="relative">
              <div className="relative bg-white/10 backdrop-blur-sm rounded-2xl p-2 transform rotate-1 hover:rotate-0 transition-transform duration-500">
                <div className="bg-white rounded-xl overflow-hidden shadow-2xl">
                  <img 
                    src="https://images.unsplash.com/photo-1503454537195-1dcabb73ffb9?w=800&h=600&fit=crop&crop=face" 
                    alt="Jesus ensinando crianças" 
                    className="w-full h-auto object-cover"
                  />
                </div>
                <div className="absolute -top-3 -right-3 bg-secondary-500 text-white px-4 py-2 rounded-full font-bold shadow-lg flex items-center gap-2">
                  <Award className="w-4 h-4" />
                  Material Testado ✓
                </div>
              </div>
            </div>
          </div>
        </div>
      </header>

      {/* Resto do seu código vai aqui... */}
      {/* Vou manter o resto do código similar ao que você já tem, mas adaptado para TypeScript */}

      {/* Modal para Material Gratuito */}
      {showFreeModal && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm">
          <div className="modal-content animate-slide-up">
            <button 
              onClick={() => setShowFreeModal(false)}
              className="absolute top-4 right-4 text-gray-500 hover:text-gray-700 transition-colors"
            >
              ✕
            </button>
            
            <div className="text-center mb-6">
              <div className="w-12 h-12 bg-secondary-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <Download className="w-6 h-6 text-secondary-600" />
              </div>
              <h3 className="text-2xl font-bold text-gray-800">
                🎁 Receba Sua Lição Gratuita
              </h3>
              <p className="text-gray-600 mt-2">
                Preencha os dados abaixo e receba imediatamente em seu e-mail:
              </p>
            </div>
            
            <form onSubmit={form.handleSubmit} className="space-y-4">
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">
                  Nome Completo *
                </label>
                <input
                  type="text"
                  name="nome"
                  value={form.values.nome}
                  onChange={form.handleChange}
                  className="input-field"
                  placeholder="Seu nome"
                />
                {form.errors.nome && (
                  <p className="mt-1 text-sm text-red-600">{form.errors.nome}</p>
                )}
              </div>
              
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">
                  E-mail *
                </label>
                <input
                  type="email"
                  name="email"
                  value={form.values.email}
                  onChange={form.handleChange}
                  className="input-field"
                  placeholder="seu@email.com"
                />
                {form.errors.email && (
                  <p className="mt-1 text-sm text-red-600">{form.errors.email}</p>
                )}
              </div>
              
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">
                  WhatsApp (opcional)
                </label>
                <input
                  type="tel"
                  name="whatsapp"
                  value={form.values.whatsapp}
                  onChange={form.handleChange}
                  className="input-field"
                  placeholder="(14) 99999-9999"
                />
              </div>
              
              <button
                type="submit"
                disabled={form.isSubmitting}
                className="btn-primary w-full py-4 text-lg"
              >
                {form.isSubmitting ? 'Enviando...' : 'Enviar e Receber Material Grátis'}
              </button>
              
              <p className="text-xs text-gray-500 text-center">
                🔒 Seus dados estão seguros. Não compartilhamos com terceiros.
              </p>
            </form>
          </div>
        </div>
      )}
    </div>
  );
}
7. EXECUTAR O PROJETO
bash
# Na pasta lpremaviva/frontend
npm run dev
O servidor vai iniciar em http://localhost:5173

8. ESTRUTURA FINAL DA PASTA FRONTEND
text
lpremaviva/frontend/
├── node_modules/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── ui/
│   │   └── sections/
│   ├── hooks/
│   │   ├── useCountdown.ts
│   │   └── useForm.ts
│   ├── services/
│   ├── types/
│   │   └── index.ts
│   ├── utils/
│   │   └── constants.ts
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── .eslintrc.cjs
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
├── postcss.config.js
├── tailwind.config.js
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts
9. PRÓXIMOS PASSOS
Terminar de copiar seu código - Substitua o App.tsx pelo seu código completo

Configurar Google Forms - Atualizar a função de submit no modal

Configurar Pagar.me - Implement


Continuar

