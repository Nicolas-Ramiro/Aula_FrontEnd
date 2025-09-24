// Estrutura do projeto (crie os arquivos conforme abaixo)

/*
project-root/
├─ package.json
├─ tailwind.config.js
├─ postcss.config.js
├─ tsconfig.json
├─ public/
│  └─ index.html
└─ src/
   ├─ main.tsx
   ├─ App.tsx
   ├─ types.ts
   ├─ data/
   │  └─ news.tsx
   ├─ pages/
   │  ├─ HomePage.tsx
   │  └─ NewsPage.tsx
   └─ components/
      ├─ Header.tsx
      ├─ Footer.tsx
      ├─ SearchBar.tsx
      ├─ NewsList.tsx
      ├─ NewsCard.tsx
      ├─ NewsDetail.tsx
      └─ Comments.tsx
*/

// package.json (dependências principais)
{
  "name": "projeto-noticias",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.14.1"
  },
  "devDependencies": {
    "@types/react": "^18.0.28",
    "@types/react-dom": "^18.0.11",
    "typescript": "^5.1.6",
    "vite": "^5.0.0",
    "tailwindcss": "^3.4.0",
    "postcss": "^8.4.0",
    "autoprefixer": "^10.4.0"
  }
}

// tailwind.config.js
module.exports = {
  content: ['./index.html', './src/**/*.{ts,tsx}'],
  theme: { extend: {} },
  plugins: [],
}

// postcss.config.js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}

// src/types.ts
export type Comment = {
  id: string;
  name: string;
  text: string;
};

export type News = {
  id: string;
  title: string;
  date: string; // ISO string or formatted
  content: string;
  image?: string;
  categories: string[];
  comments?: Comment[];
};

// src/data/news.tsx  (array estático com pelo menos 10 notícias)
import { News } from '../types';

export const NEWS: News[] = [
  {
    id: '1',
    title: 'Novo centro comunitário abre na cidade',
    date: '2025-06-01',
    content: 'Foi inaugurado um novo centro comunitário para atender programas sociais e culturais. O espaço contará com oficinas, eventos e apoio a famílias.',
    image: '/placeholder-1.jpg',
    categories: ['Sociedade', 'Cultura'],
    comments: [
      { id: 'c1', name: 'João', text: 'Ótima iniciativa!' },
    ],
  },
  {
    id: '2',
    title: 'Feira de tecnologia reúne startups locais',
    date: '2025-06-02',
    content: 'Startups locais apresentam soluções inovadoras para educação e saúde na feira anual.',
    image: '/placeholder-2.jpg',
    categories: ['Tecnologia'],
  },
  {
    id: '3',
    title: 'Campanha de doação de sangue supera meta',
    date: '2025-06-03',
    content: 'A campanha atingiu a meta do mês e ajudará hospitais da região.',
    image: '/placeholder-3.jpg',
    categories: ['Saúde'],
  },
  {
    id: '4',
    title: 'Prefeitura anuncia melhorias no transporte público',
    date: '2025-06-04',
    content: 'Novas linhas e horários foram divulgados para melhorar a mobilidade urbana.',
    image: '/placeholder-4.jpg',
    categories: ['Política', 'Transporte'],
  },
  {
    id: '5',
    title: 'Biblioteca pública ganha acervo digital',
    date: '2025-06-05',
    content: 'Os moradores poderão acessar milhares de títulos em formato digital.',
    categories: ['Cultura', 'Educação'],
  },
  {
    id: '6',
    title: 'Festival gastronômico terá chefs convidados',
    date: '2025-06-06',
    content: 'O evento reunirá chefs locais e regionais com pratos autorais.',
    categories: ['Cultura', 'Gastronomia'],
  },
  {
    id: '7',
    title: 'Escola adota projeto de sustentabilidade',
    date: '2025-06-07',
    content: 'Alunos participarão de plantio de árvores e reciclagem.',
    categories: ['Educação', 'Meio Ambiente'],
  },
  {
    id: '8',
    title: 'Time local avança no campeonato',
    date: '2025-06-08',
    content: 'Vitória histórica garante vaga nas semifinais.',
    categories: ['Esporte'],
  },
  {
    id: '9',
    title: 'Exposição de arte traz artistas emergentes',
    date: '2025-06-09',
    content: 'A mostra apresenta pinturas, esculturas e instalações.',
    categories: ['Arte', 'Cultura'],
  },
  {
    id: '10',
    title: 'Projeto de saúde mental chega a mais bairros',
    date: '2025-06-10',
    content: 'Atendimento gratuito será oferecido em unidades de saúde.',
    categories: ['Saúde'],
  },
];

// src/main.tsx
import React from 'react'
import { createRoot } from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'
import './index.css'

createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
)

// src/index.css
@tailwind base;
@tailwind components;
@tailwind utilities;

html, body, #root { height: 100%; }

// src/App.tsx
import React from 'react'
import { Routes, Route } from 'react-router-dom'
import HomePage from './pages/HomePage'
import NewsPage from './pages/NewsPage'
import Header from './components/Header'
import Footer from './components/Footer'

export default function App() {
  return (
    <div className="min-h-screen flex flex-col">
      <Header />
      <main className="flex-1 container mx-auto px-4 py-6">
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/news/:id" element={<NewsPage />} />
        </Routes>
      </main>
      <Footer />
    </div>
  )
}

// src/components/Header.tsx
import React from 'react'
import { Link } from 'react-router-dom'

export default function Header(){
  return (
    <header className="bg-white shadow">
      <div className="container mx-auto px-4 py-4 flex items-center justify-between">
        <Link to="/" className="text-xl font-semibold">Resgate+</Link>
        <nav className="hidden md:flex gap-4">
          <Link to="/" className="hover:underline">Home</Link>
        </nav>
      </div>
    </header>
  )
}

// src/components/Footer.tsx
import React from 'react'

export default function Footer(){
  return (
    <footer className="bg-gray-800 text-white py-6 mt-8">
      <div className="container mx-auto px-4 text-center">
        <p>© 2025 Resgate+ - Projeto de exemplo</p>
      </div>
    </footer>
  )
}

// src/components/SearchBar.tsx
import React from 'react'

type Props = {
  value: string;
  onChange: (v: string) => void;
}

export default function SearchBar({value, onChange}: Props){
  return (
    <div className="mb-4">
      <input
        aria-label="Pesquisar notícias"
        value={value}
        onChange={(e)=>onChange(e.target.value)}
        placeholder="Filtrar por título, conteúdo ou categoria"
        className="w-full border rounded px-3 py-2"
      />
    </div>
  )
}

// src/components/NewsCard.tsx
import React from 'react'
import { News } from '../types'
import { Link } from 'react-router-dom'

function truncate(text: string, max = 50){
  if(text.length <= max) return text
  return text.slice(0, max) + '...'
}

export default function NewsCard({item}:{item: News}){
  return (
    <article className="border rounded overflow-hidden shadow-sm hover:shadow-md transition">
      <div className="p-4">
        <h3 className="text-lg font-semibold mb-1"><Link to={`/news/${item.id}`}>{item.title}</Link></h3>
        <p className="text-sm text-gray-500 mb-2">{item.date}</p>
        <p className="text-gray-700">{truncate(item.content, 50)}</p>
        <div className="mt-3 text-sm">
          {item.categories.map(c=> (
            <span key={c} className="inline-block mr-2 px-2 py-1 bg-gray-100 rounded">{c}</span>
          ))}
        </div>
      </div>
    </article>
  )
}

// src/components/NewsList.tsx
import React from 'react'
import { News } from '../types'
import NewsCard from './NewsCard'

export default function NewsList({items}:{items: News[]}){
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      {items.map(i=> <NewsCard key={i.id} item={i} />)}
    </div>
  )
}

// src/pages/HomePage.tsx
import React, { useMemo, useState } from 'react'
import { NEWS } from '../data/news'
import SearchBar from '../components/SearchBar'
import NewsList from '../components/NewsList'

export default function HomePage(){
  const [filter, setFilter] = useState('')

  const filtered = useMemo(()=>{
    const q = filter.trim().toLowerCase()
    if(!q) return NEWS
    return NEWS.filter(n=>
      n.title.toLowerCase().includes(q)
      || n.content.toLowerCase().includes(q)
      || n.categories.join(' ').toLowerCase().includes(q)
    )
  }, [filter])

  return (
    <div>
      <h1 className="text-2xl font-bold mb-4">Notícias</h1>
      <SearchBar value={filter} onChange={setFilter} />

      {filtered.length === 0 ? (
        <p>Nenhum artigo encontrado.</p>
      ) : (
        <NewsList items={filtered} />
      )}
    </div>
  )
}

// src/pages/NewsPage.tsx
import React from 'react'
import { useParams, Link, useNavigate } from 'react-router-dom'
import { NEWS } from '../data/news'
import NewsDetail from '../components/NewsDetail'

export default function NewsPage(){
  const { id } = useParams()
  const navigate = useNavigate()
  const item = NEWS.find(n=> n.id === id)

  if(!item) return (
    <div>
      <p>Notícia não encontrada.</p>
      <button className="mt-4 px-4 py-2 border rounded" onClick={()=>navigate(-1)}>Voltar</button>
    </div>
  )

  return (
    <div>
      <Link to="/" className="text-sm text-blue-600 underline">&larr; Voltar para a home</Link>
      <NewsDetail item={item} />
    </div>
  )
}

// src/components/NewsDetail.tsx
import React from 'react'
import { News } from '../types'
import Comments from './Comments'

export default function NewsDetail({item}:{item: News}){
  return (
    <article className="mt-4">
      <h2 className="text-2xl font-bold mb-1">{item.title}</h2>
      <p className="text-sm text-gray-500 mb-4">{item.date}</p>
      {item.image && <img src={item.image} alt="" className="w-full max-h-64 object-cover mb-4 rounded" />}
      <div className="prose max-w-none mb-6">{item.content}</div>
      <section>
        <h3 className="text-lg font-semibold mb-2">Comentários</h3>
        <Comments initialComments={item.comments ?? []} />
      </section>
    </article>
  )
}

// src/components/Comments.tsx
import React, { useEffect, useState } from 'react'
import { Comment } from '../types'

export default function Comments({initialComments}:{initialComments: Comment[]}){
  const [comments, setComments] = useState<Comment[]>([])
  const [loading, setLoading] = useState(true)
  const [name, setName] = useState('')
  const [text, setText] = useState('')

  // Simula carregamento do componente de comentários depois do carregamento inicial
  useEffect(()=>{
    const t = setTimeout(()=>{
      setComments(initialComments)
      setLoading(false)
    }, 600) // simula carregamento
    return ()=>clearTimeout(t)
  }, [initialComments])

  function addComment(e: React.FormEvent){
    e.preventDefault()
    if(!name.trim() || !text.trim()) return
    const c: Comment = { id: String(Date.now()), name: name.trim(), text: text.trim() }
    setComments(prev=>[...prev, c])
    setName('')
    setText('')
  }

  if(loading) return <p>Carregando comentários...</p>

  return (
    <div>
      <ul className="space-y-3 mb-4">
        {comments.length === 0 ? <li className="text-sm text-gray-600">Sem comentários ainda.</li> : comments.map(c=> (
          <li key={c.id} className="border p-3 rounded">
            <p className="font-semibold">{c.name}</p>
            <p>{c.text}</p>
          </li>
        ))}
      </ul>

      <form onSubmit={addComment} className="space-y-2">
        <input value={name} onChange={e=>setName(e.target.value)} placeholder="Nome" className="w-full border rounded px-2 py-1" />
        <textarea value={text} onChange={e=>setText(e.target.value)} placeholder="Comentário" className="w-full border rounded px-2 py-1" />
        <button className="px-4 py-2 bg-blue-600 text-white rounded">Enviar comentário</button>
      </form>
    </div>
  )
}

/*
Observações finais:
- O array de notícias estático está em src/data/news.tsx e tem 10 itens.
- A home filtra por título, conteúdo e categorias. Exibe mensagem "Nenhum artigo encontrado." quando não há resultados.
- A exibição do conteúdo na home usa truncamento para no máximo 50 caracteres conforme solicitado.
- Os comentários são carregados e renderizados em um componente isolado após o carregamento inicial da página.

Você pode colar estes arquivos no seu projeto Vite + React + TypeScript e executar.
*/
