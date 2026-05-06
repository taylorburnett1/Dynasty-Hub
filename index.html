import React, { useState, useEffect, useMemo } from 'react';
import { Plus, Search, X, ExternalLink, Trash2, Edit2, FolderPlus, Check, Trophy, Users, Zap, GraduationCap, Folder, Sparkles, Calendar, Lightbulb, DoorOpen } from 'lucide-react';

const DEFAULT_CATEGORIES = [
  { name: 'Leaderboard', icon: 'trophy' },
  { name: 'Leadership', icon: 'users' },
  { name: 'DBD', icon: 'zap' },
  { name: 'Trainings', icon: 'graduation' },
  { name: 'Sunday Planning', icon: 'calendar' },
  { name: 'Tips and Tricks', icon: 'lightbulb' },
  { name: 'The Door Knock', icon: 'door' },
];

const ICON_MAP = {
  trophy: Trophy,
  users: Users,
  zap: Zap,
  graduation: GraduationCap,
  folder: Folder,
  sparkles: Sparkles,
  calendar: Calendar,
  lightbulb: Lightbulb,
  door: DoorOpen,
};

const ICON_OPTIONS = ['trophy', 'users', 'zap', 'graduation', 'calendar', 'lightbulb', 'door', 'folder', 'sparkles'];

const uid = () => Math.random().toString(36).slice(2, 10);

const tidyUrl = (u) => {
  if (!u) return '';
  if (!/^https?:\/\//i.test(u)) return 'https://' + u;
  return u;
};

const getDomain = (url) => {
  try { return new URL(tidyUrl(url)).hostname.replace(/^www\./, ''); }
  catch { return ''; }
};

export default function DynastyHub() {
  const [links, setLinks] = useState([]);
  const [categories, setCategories] = useState(DEFAULT_CATEGORIES);
  const [activeCategory, setActiveCategory] = useState('All');
  const [activeTags, setActiveTags] = useState([]);
  const [search, setSearch] = useState('');
  const [showAdd, setShowAdd] = useState(false);
  const [editing, setEditing] = useState(null);
  const [loading, setLoading] = useState(true);
  const [saveStatus, setSaveStatus] = useState('');
  const [showNewCat, setShowNewCat] = useState(false);
  const [newCatName, setNewCatName] = useState('');
  const [newCatIcon, setNewCatIcon] = useState('folder');

  const [form, setForm] = useState({ title: '', url: '', category: 'Leaderboard', tags: '' });

  useEffect(() => {
    (async () => {
      try {
        const l = await window.storage.get('dh_links').catch(() => null);
        const c = await window.storage.get('dh_categories').catch(() => null);
        if (l?.value) setLinks(JSON.parse(l.value));
        if (c?.value) {
          const parsed = JSON.parse(c.value);
          setCategories(parsed.map(x => typeof x === 'string' ? { name: x, icon: 'folder' } : x));
        }
      } catch (e) {}
      setLoading(false);
    })();
  }, []);

  useEffect(() => {
    if (loading) return;
    const t = setTimeout(async () => {
      setSaveStatus('saving');
      try {
        await window.storage.set('dh_links', JSON.stringify(links));
        await window.storage.set('dh_categories', JSON.stringify(categories));
        setSaveStatus('saved');
        setTimeout(() => setSaveStatus(''), 1200);
      } catch { setSaveStatus('error'); }
    }, 400);
    return () => clearTimeout(t);
  }, [links, categories, loading]);

  const allTags = useMemo(() => {
    const s = new Set();
    links.forEach(l => l.tags?.forEach(t => s.add(t)));
    return [...s].sort();
  }, [links]);

  const filtered = useMemo(() => {
    return links.filter(l => {
      if (activeCategory !== 'All' && l.category !== activeCategory) return false;
      if (activeTags.length && !activeTags.every(t => l.tags?.includes(t))) return false;
      if (search) {
        const q = search.toLowerCase();
        if (!l.title.toLowerCase().includes(q) && !l.url.toLowerCase().includes(q)) return false;
      }
      return true;
    });
  }, [links, activeCategory, activeTags, search]);

  const counts = useMemo(() => {
    const c = { All: links.length };
    categories.forEach(cat => { c[cat.name] = links.filter(l => l.category === cat.name).length; });
    return c;
  }, [links, categories]);

  const openForm = (link = null) => {
    if (link) {
      setForm({ title: link.title, url: link.url, category: link.category, tags: link.tags?.join(', ') || '' });
      setEditing(link.id);
    } else {
      const cat = activeCategory !== 'All' ? activeCategory : (categories[0]?.name || 'Leaderboard');
      setForm({ title: '', url: '', category: cat, tags: '' });
      setEditing(null);
    }
    setShowAdd(true);
  };

  const closeForm = () => {
    setShowAdd(false);
    setEditing(null);
    setForm({ title: '', url: '', category: 'Leaderboard', tags: '' });
  };

  const saveLink = () => {
    if (!form.title.trim() || !form.url.trim()) return;
    const tags = form.tags.split(',').map(t => t.trim()).filter(Boolean);
    const data = {
      title: form.title.trim(),
      url: tidyUrl(form.url.trim()),
      category: form.category,
      tags,
    };
    if (editing) {
      setLinks(prev => prev.map(l => l.id === editing ? { ...l, ...data } : l));
    } else {
      setLinks(prev => [{ id: uid(), ...data, created: Date.now() }, ...prev]);
    }
    closeForm();
  };

  const deleteLink = (id) => {
    if (!confirm('Delete this link?')) return;
    setLinks(prev => prev.filter(l => l.id !== id));
  };

  const toggleTag = (t) => {
    setActiveTags(prev => prev.includes(t) ? prev.filter(x => x !== t) : [...prev, t]);
  };

  const addCategory = () => {
    const name = newCatName.trim();
    if (!name || categories.find(c => c.name === name)) {
      setShowNewCat(false); setNewCatName(''); setNewCatIcon('folder');
      return;
    }
    setCategories(prev => [...prev, { name, icon: newCatIcon }]);
    setNewCatName('');
    setNewCatIcon('folder');
    setShowNewCat(false);
    setActiveCategory(name);
  };

  const deleteCategory = (catName) => {
    const inUse = links.filter(l => l.category === catName).length;
    if (inUse && !confirm(`${inUse} link(s) use "${catName}". Delete category? Links will be unassigned.`)) return;
    setCategories(prev => prev.filter(c => c.name !== catName));
    setLinks(prev => prev.map(l => l.category === catName ? { ...l, category: '' } : l));
    if (activeCategory === catName) setActiveCategory('All');
  };

  const getCategoryIcon = (catName) => {
    const cat = categories.find(c => c.name === catName);
    return cat ? ICON_MAP[cat.icon] || Folder : Folder;
  };

  return (
    <div style={{ minHeight: '100vh', background: '#0b1220', color: '#e8edf5', fontFamily: '"Inter", system-ui, sans-serif', position: 'relative', overflow: 'hidden' }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&family=JetBrains+Mono:wght@400;500;600&family=Inter:wght@400;500;600;700&display=swap');
        * { box-sizing: border-box; }
        .display-font { font-family: 'Fraunces', serif; font-variation-settings: 'opsz' 144; letter-spacing: -0.02em; }
        .mono-font { font-family: 'JetBrains Mono', monospace; }

        .bg-glow {
          position: fixed; inset: 0; pointer-events: none; z-index: 0;
          background:
            radial-gradient(900px circle at 12% 8%, rgba(56, 189, 248, 0.12), transparent 50%),
            radial-gradient(700px circle at 88% 92%, rgba(168, 85, 247, 0.08), transparent 50%);
        }
        .grid-overlay {
          position: fixed; inset: 0; pointer-events: none; z-index: 0;
          background-image:
            linear-gradient(rgba(255,255,255,0.015) 1px, transparent 1px),
            linear-gradient(90deg, rgba(255,255,255,0.015) 1px, transparent 1px);
          background-size: 60px 60px;
        }
        .content { position: relative; z-index: 1; }

        .field {
          background: rgba(15, 23, 42, 0.6);
          border: 1px solid rgba(148, 163, 184, 0.15);
          color: #e8edf5;
          padding: 11px 14px;
          font-family: 'Inter', sans-serif;
          font-size: 14px;
          width: 100%;
          transition: all 0.2s;
          border-radius: 10px;
          backdrop-filter: blur(8px);
        }
        .field:focus {
          outline: none;
          border-color: #38bdf8;
          background: rgba(15, 23, 42, 0.9);
          box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.12);
        }
        .field::placeholder { color: #475569; }

        .btn-primary {
          background: linear-gradient(135deg, #38bdf8 0%, #0ea5e9 100%);
          color: #0b1220;
          border: none;
          padding: 11px 20px;
          font-family: 'Inter', sans-serif;
          font-size: 13px;
          font-weight: 600;
          cursor: pointer;
          border-radius: 10px;
          display: inline-flex;
          align-items: center;
          gap: 8px;
          transition: all 0.2s;
          box-shadow: 0 4px 14px rgba(56, 189, 248, 0.3);
        }
        .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(56, 189, 248, 0.4); }
        .btn-primary:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

        .btn-ghost {
          background: transparent;
          border: 1px solid rgba(148, 163, 184, 0.2);
          color: #94a3b8;
          padding: 9px 16px;
          font-family: 'Inter', sans-serif;
          font-size: 13px;
          font-weight: 500;
          cursor: pointer;
          border-radius: 10px;
          display: inline-flex;
          align-items: center;
          gap: 6px;
          transition: all 0.2s;
        }
        .btn-ghost:hover { border-color: rgba(56, 189, 248, 0.4); color: #38bdf8; }

        .cat-btn {
          background: transparent;
          border: 1px solid transparent;
          color: #94a3b8;
          padding: 11px 14px;
          font-family: 'Inter', sans-serif;
          font-size: 14px;
          font-weight: 500;
          cursor: pointer;
          border-radius: 10px;
          display: flex;
          align-items: center;
          justify-content: space-between;
          width: 100%;
          margin-bottom: 4px;
          transition: all 0.18s;
          gap: 10px;
        }
        .cat-btn:hover { background: rgba(56, 189, 248, 0.06); color: #e8edf5; }
        .cat-btn.active {
          background: linear-gradient(135deg, rgba(56, 189, 248, 0.15) 0%, rgba(56, 189, 248, 0.05) 100%);
          border-color: rgba(56, 189, 248, 0.3);
          color: #38bdf8;
        }
        .cat-btn .count {
          font-family: 'JetBrains Mono';
          font-size: 11px;
          color: #475569;
          background: rgba(148, 163, 184, 0.08);
          padding: 2px 8px;
          border-radius: 6px;
        }
        .cat-btn.active .count { color: #38bdf8; background: rgba(56, 189, 248, 0.15); }

        .tag-pill {
          display: inline-flex; align-items: center; gap: 4px;
          background: rgba(148, 163, 184, 0.06);
          border: 1px solid rgba(148, 163, 184, 0.12);
          color: #94a3b8;
          padding: 4px 10px;
          font-family: 'JetBrains Mono';
          font-size: 11px;
          cursor: pointer;
          border-radius: 999px;
          transition: all 0.15s;
        }
        .tag-pill:hover { border-color: rgba(56, 189, 248, 0.4); color: #38bdf8; }
        .tag-pill.active {
          background: rgba(56, 189, 248, 0.15);
          border-color: #38bdf8;
          color: #38bdf8;
        }

        .link-card {
          background: rgba(15, 23, 42, 0.5);
          border: 1px solid rgba(148, 163, 184, 0.12);
          padding: 18px;
          border-radius: 14px;
          transition: all 0.2s;
          position: relative;
          display: flex;
          flex-direction: column;
          gap: 12px;
          backdrop-filter: blur(8px);
          overflow: hidden;
        }
        .link-card::before {
          content: '';
          position: absolute;
          top: 0; left: 0; right: 0;
          height: 1px;
          background: linear-gradient(90deg, transparent, rgba(56, 189, 248, 0), transparent);
          transition: all 0.4s;
        }
        .link-card:hover {
          border-color: rgba(56, 189, 248, 0.3);
          transform: translateY(-2px);
          box-shadow: 0 12px 30px -10px rgba(0, 0, 0, 0.4);
        }
        .link-card:hover::before {
          background: linear-gradient(90deg, transparent, rgba(56, 189, 248, 0.6), transparent);
        }
        .link-card .actions { opacity: 0; transition: opacity 0.15s; }
        .link-card:hover .actions { opacity: 1; }

        .icon-btn {
          background: transparent; border: none; color: #64748b; cursor: pointer;
          padding: 6px; border-radius: 6px; display: inline-flex;
          transition: all 0.15s;
        }
        .icon-btn:hover { color: #38bdf8; background: rgba(56, 189, 248, 0.08); }
        .icon-btn.danger:hover { color: #f87171; background: rgba(248, 113, 113, 0.08); }

        .modal-bg {
          position: fixed; inset: 0;
          background: rgba(8, 12, 22, 0.7);
          backdrop-filter: blur(8px);
          display: flex; align-items: center; justify-content: center;
          z-index: 100; padding: 20px;
        }
        .modal {
          background: linear-gradient(180deg, #0f172a 0%, #0b1220 100%);
          border: 1px solid rgba(148, 163, 184, 0.15);
          padding: 32px;
          border-radius: 18px;
          width: 100%; max-width: 480px;
          box-shadow: 0 24px 60px rgba(0,0,0,0.5), 0 0 0 1px rgba(56, 189, 248, 0.08);
        }
        .label {
          font-family: 'Inter', sans-serif;
          font-size: 12px;
          color: #94a3b8;
          font-weight: 500;
          margin-bottom: 8px;
          display: block;
        }

        .icon-picker {
          display: flex; gap: 6px; flex-wrap: wrap;
        }
        .icon-pick {
          width: 38px; height: 38px;
          background: rgba(15, 23, 42, 0.6);
          border: 1px solid rgba(148, 163, 184, 0.15);
          border-radius: 8px;
          display: flex; align-items: center; justify-content: center;
          cursor: pointer;
          color: #64748b;
          transition: all 0.15s;
        }
        .icon-pick:hover { border-color: rgba(56, 189, 248, 0.4); color: #38bdf8; }
        .icon-pick.active {
          background: rgba(56, 189, 248, 0.15);
          border-color: #38bdf8;
          color: #38bdf8;
        }

        .layout { display: grid; grid-template-columns: 260px 1fr; gap: 36px; }
        @media (max-width: 800px) {
          .layout { grid-template-columns: 1fr; gap: 24px; }
          .header-grid { grid-template-columns: 1fr !important; }
          .grid-cards { grid-template-columns: 1fr !important; }
          .hero-title { font-size: 56px !important; }
        }

        select.field {
          appearance: none;
          background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%2394a3b8' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E");
          background-repeat: no-repeat;
          background-position: right 14px center;
          padding-right: 36px;
        }
      `}</style>

      <div className="bg-glow" />
      <div className="grid-overlay" />

      <div className="content">
        {/* Header */}
        <div style={{ borderBottom: '1px solid rgba(148, 163, 184, 0.1)' }}>
          <div style={{ maxWidth: 1280, margin: '0 auto', padding: '40px 24px' }}>
            <div className="header-grid" style={{ display: 'grid', gridTemplateColumns: '1fr auto', gap: 24, alignItems: 'end' }}>
              <div>
                <div className="mono-font" style={{ fontSize: 11, color: '#38bdf8', letterSpacing: '0.25em', marginBottom: 12, display: 'flex', alignItems: 'center', gap: 8 }}>
                  <span style={{ width: 6, height: 6, background: '#38bdf8', borderRadius: '50%', boxShadow: '0 0 12px #38bdf8' }} />
                  COMMAND CENTER
                </div>
                <div style={{ display: 'flex', alignItems: 'center', gap: 20 }}>
                  <svg viewBox="0 0 1071 1028" width="92" height="92" style={{ flexShrink: 0, filter: 'drop-shadow(0 0 24px rgba(56, 189, 248, 0.35))' }} xmlns="http://www.w3.org/2000/svg">
                    <defs>
                      <linearGradient id="dGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stopColor="#38bdf8" />
                        <stop offset="100%" stopColor="#a855f7" />
                      </linearGradient>
                    </defs>
                    <g transform="translate(-109.921448,1120.703960) scale(0.1,-0.1)" fill="url(#dGrad)">
                      <path d="M6075 11203 c-148 -7 -557 -45 -705 -64 -1277 -163 -2441 -695 -3254 -1489 -515 -502 -854 -1068 -971 -1620 -43 -200 -58 -534 -35 -745 46 -412 194 -749 434 -991 251 -252 571 -386 956 -401 551 -21 992 254 1264 787 187 366 268 841 201 1165 -16 75 -44 155 -54 155 -4 0 -27 -30 -51 -67 -156 -237 -383 -432 -584 -500 -102 -35 -240 -39 -324 -10 -280 98 -380 486 -236 917 168 506 584 1021 1149 1420 210 148 540 329 815 445 654 276 1469 413 2182 365 228 -16 677 -76 695 -93 2 -2 -30 -16 -69 -32 -188 -72 -497 -249 -673 -384 -288 -221 -543 -486 -751 -781 -225 -319 -460 -794 -607 -1230 -117 -344 -231 -782 -321 -1231 -43 -215 -149 -846 -211 -1259 -124 -828 -254 -1408 -445 -1995 -87 -266 -139 -397 -155 -391 -66 25 -324 103 -417 126 -693 170 -1427 64 -1943 -281 -129 -86 -294 -247 -373 -361 -308 -450 -272 -983 90 -1339 211 -208 540 -342 933 -380 146 -14 430 -6 570 16 437 69 866 260 1220 544 137 109 359 333 497 499 l27 33 113 -62 c754 -412 1281 -589 1913 -640 214 -17 650 -7 830 20 451 67 793 173 1212 376 452 219 817 480 1194 855 431 429 795 957 1067 1550 315 687 491 1359 542 2075 13 182 13 616 0 781 -13 162 -44 403 -71 542 -261 1372 -1160 2538 -2434 3153 -582 281 -1196 439 -1970 505 -171 15 -1067 27 -1250 17z m2357 -1107 c374 -72 903 -490 1229 -972 122 -181 269 -453 340 -632 320 -795 383 -1791 178 -2806 -135 -668 -490 -1440 -922 -2006 -505 -660 -1042 -1041 -1711 -1214 -199 -52 -329 -67 -603 -73 -408 -9 -671 29 -1103 159 -112 33 -408 135 -418 143 -2 1 53 87 121 191 185 283 239 375 377 649 369 731 554 1427 770 2900 47 326 72 472 141 835 285 1490 614 2298 1081 2650 132 99 228 147 353 175 78 17 80 17 167 1z m-4766 -7531 c107 -16 330 -68 341 -79 16 -16 -117 -195 -242 -325 -249 -258 -531 -385 -855 -384 -171 0 -274 32 -362 111 -106 95 -108 257 -5 393 81 109 201 188 367 243 92 30 155 43 300 60 69 8 357 -4 456 -19z" />
                    </g>
                  </svg>
                  <h1 className="display-font hero-title" style={{ fontSize: 84, lineHeight: 0.92, margin: 0, color: '#f8fafc', fontWeight: 600 }}>
                    Dynasty <span style={{ fontStyle: 'italic', background: 'linear-gradient(135deg, #38bdf8, #a855f7)', WebkitBackgroundClip: 'text', WebkitTextFillColor: 'transparent', paddingRight: '0.15em', display: 'inline-block' }}>Hub</span>
                  </h1>
                </div>
                <div style={{ fontSize: 14, color: '#64748b', marginTop: 14, fontWeight: 400 }}>
                  {links.length} {links.length === 1 ? 'link' : 'links'} · {categories.length} categories · {allTags.length} tags
                </div>
              </div>
              <div style={{ display: 'flex', gap: 12, alignItems: 'center' }}>
                {saveStatus && (
                  <span className="mono-font" style={{ fontSize: 11, color: saveStatus === 'saved' ? '#38bdf8' : '#64748b', display: 'flex', alignItems: 'center', gap: 6 }}>
                    <span style={{ width: 5, height: 5, background: saveStatus === 'saved' ? '#38bdf8' : '#64748b', borderRadius: '50%' }} />
                    {saveStatus}
                  </span>
                )}
                <button className="btn-primary" onClick={() => openForm()}>
                  <Plus size={15} /> Add Link
                </button>
              </div>
            </div>
          </div>
        </div>

        {/* Body */}
        <div style={{ maxWidth: 1280, margin: '0 auto', padding: '36px 24px 80px' }}>
          <div className="layout">
            {/* Sidebar */}
            <aside>
              {/* Search */}
              <div style={{ position: 'relative', marginBottom: 24 }}>
                <Search size={15} style={{ position: 'absolute', left: 14, top: '50%', transform: 'translateY(-50%)', color: '#475569' }} />
                <input
                  className="field"
                  style={{ paddingLeft: 38 }}
                  placeholder="Search links..."
                  value={search}
                  onChange={(e) => setSearch(e.target.value)}
                />
                {search && (
                  <button onClick={() => setSearch('')} style={{ position: 'absolute', right: 8, top: '50%', transform: 'translateY(-50%)', background: 'transparent', border: 'none', color: '#64748b', cursor: 'pointer', padding: 4 }}>
                    <X size={14} />
                  </button>
                )}
              </div>

              {/* Categories */}
              <div style={{ marginBottom: 28 }}>
                <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 12 }}>
                  <span style={{ fontSize: 11, color: '#64748b', letterSpacing: '0.15em', textTransform: 'uppercase', fontWeight: 600 }}>Categories</span>
                  <button className="icon-btn" onClick={() => setShowNewCat(true)} title="Add category">
                    <FolderPlus size={14} />
                  </button>
                </div>

                <button className={`cat-btn ${activeCategory === 'All' ? 'active' : ''}`} onClick={() => setActiveCategory('All')}>
                  <span style={{ display: 'flex', alignItems: 'center', gap: 10 }}>
                    <Sparkles size={14} /> All
                  </span>
                  <span className="count">{counts.All || 0}</span>
                </button>

                {categories.map(cat => {
                  const Icon = ICON_MAP[cat.icon] || Folder;
                  return (
                    <button key={cat.name} className={`cat-btn ${activeCategory === cat.name ? 'active' : ''}`} onClick={() => setActiveCategory(cat.name)}>
                      <span style={{ display: 'flex', alignItems: 'center', gap: 10 }}>
                        <Icon size={14} /> {cat.name}
                      </span>
                      <span className="count">{counts[cat.name] || 0}</span>
                    </button>
                  );
                })}

                {showNewCat && (
                  <div style={{ marginTop: 10, padding: 12, background: 'rgba(15, 23, 42, 0.5)', borderRadius: 10, border: '1px solid rgba(148, 163, 184, 0.15)' }}>
                    <input
                      className="field"
                      autoFocus
                      placeholder="Category name"
                      value={newCatName}
                      onChange={(e) => setNewCatName(e.target.value)}
                      onKeyDown={(e) => { if (e.key === 'Enter') addCategory(); if (e.key === 'Escape') { setShowNewCat(false); setNewCatName(''); } }}
                      style={{ fontSize: 13, marginBottom: 10 }}
                    />
                    <div className="icon-picker" style={{ marginBottom: 10 }}>
                      {ICON_OPTIONS.map(ic => {
                        const Ic = ICON_MAP[ic];
                        return (
                          <div key={ic} className={`icon-pick ${newCatIcon === ic ? 'active' : ''}`} onClick={() => setNewCatIcon(ic)}>
                            <Ic size={16} />
                          </div>
                        );
                      })}
                    </div>
                    <div style={{ display: 'flex', gap: 6 }}>
                      <button className="btn-primary" style={{ padding: '8px 14px', fontSize: 12, flex: 1 }} onClick={addCategory}>
                        <Check size={13} /> Add
                      </button>
                      <button className="btn-ghost" style={{ padding: '8px 14px', fontSize: 12 }} onClick={() => { setShowNewCat(false); setNewCatName(''); }}>
                        Cancel
                      </button>
                    </div>
                  </div>
                )}

                {activeCategory !== 'All' && categories.find(c => c.name === activeCategory) && (
                  <button
                    className="btn-ghost"
                    style={{ marginTop: 12, width: '100%', justifyContent: 'center', fontSize: 12 }}
                    onClick={() => deleteCategory(activeCategory)}
                  >
                    <Trash2 size={12} /> Delete "{activeCategory}"
                  </button>
                )}
              </div>

              {/* Tags */}
              {allTags.length > 0 && (
                <div>
                  <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 12 }}>
                    <span style={{ fontSize: 11, color: '#64748b', letterSpacing: '0.15em', textTransform: 'uppercase', fontWeight: 600 }}>Tags</span>
                    {activeTags.length > 0 && (
                      <button onClick={() => setActiveTags([])} style={{ background: 'transparent', border: 'none', color: '#64748b', cursor: 'pointer', fontSize: 11, fontFamily: 'Inter' }}>clear</button>
                    )}
                  </div>
                  <div style={{ display: 'flex', flexWrap: 'wrap', gap: 6 }}>
                    {allTags.map(t => (
                      <span key={t} className={`tag-pill ${activeTags.includes(t) ? 'active' : ''}`} onClick={() => toggleTag(t)}>
                        {t}
                      </span>
                    ))}
                  </div>
                </div>
              )}
            </aside>

            {/* Main */}
            <main>
              <div style={{ marginBottom: 24, display: 'flex', justifyContent: 'space-between', alignItems: 'baseline' }}>
                <h2 className="display-font" style={{ fontSize: 36, margin: 0, color: '#f8fafc', fontWeight: 600 }}>
                  {activeCategory === 'All' ? 'All links' : activeCategory}
                </h2>
                <span className="mono-font" style={{ fontSize: 12, color: '#64748b' }}>
                  {filtered.length} {filtered.length === 1 ? 'result' : 'results'}
                </span>
              </div>

              {filtered.length === 0 ? (
                <div style={{ padding: '80px 20px', textAlign: 'center', border: '1px dashed rgba(148, 163, 184, 0.2)', borderRadius: 14, background: 'rgba(15, 23, 42, 0.3)' }}>
                  <div className="display-font" style={{ fontSize: 32, color: '#475569', marginBottom: 8, fontWeight: 600 }}>
                    {links.length === 0 ? 'Empty hub' : 'No matches'}
                  </div>
                  <div style={{ fontSize: 14, color: '#64748b', marginBottom: 24 }}>
                    {links.length === 0 ? 'Drop your first link to get started' : 'Try clearing filters or search'}
                  </div>
                  {links.length === 0 && (
                    <button className="btn-primary" onClick={() => openForm()}>
                      <Plus size={15} /> Add First Link
                    </button>
                  )}
                </div>
              ) : (
                <div className="grid-cards" style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fill, minmax(290px, 1fr))', gap: 14 }}>
                  {filtered.map(link => {
                    const CatIcon = getCategoryIcon(link.category);
                    return (
                      <div key={link.id} className="link-card">
                        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'flex-start', gap: 8 }}>
                          <a
                            href={link.url}
                            target="_blank"
                            rel="noopener noreferrer"
                            style={{ color: '#f8fafc', textDecoration: 'none', fontWeight: 600, fontSize: 16, lineHeight: 1.35, flex: 1 }}
                          >
                            {link.title}
                          </a>
                          <div className="actions" style={{ display: 'flex', gap: 2 }}>
                            <button className="icon-btn" onClick={() => openForm(link)} title="Edit">
                              <Edit2 size={13} />
                            </button>
                            <button className="icon-btn danger" onClick={() => deleteLink(link.id)} title="Delete">
                              <Trash2 size={13} />
                            </button>
                          </div>
                        </div>

                        <a
                          href={link.url}
                          target="_blank"
                          rel="noopener noreferrer"
                          className="mono-font"
                          style={{ fontSize: 12, color: '#64748b', textDecoration: 'none', display: 'flex', alignItems: 'center', gap: 6, overflow: 'hidden', textOverflow: 'ellipsis', whiteSpace: 'nowrap' }}
                        >
                          <ExternalLink size={11} /> {getDomain(link.url)}
                        </a>

                        <div style={{ display: 'flex', flexWrap: 'wrap', gap: 6, alignItems: 'center', borderTop: '1px solid rgba(148, 163, 184, 0.08)', paddingTop: 12 }}>
                          {link.category && (
                            <span style={{ fontSize: 11, color: '#38bdf8', fontWeight: 600, display: 'inline-flex', alignItems: 'center', gap: 5, marginRight: 4 }}>
                              <CatIcon size={11} /> {link.category}
                            </span>
                          )}
                          {link.tags?.map(t => (
                            <span key={t} className="tag-pill" style={{ pointerEvents: 'none', fontSize: 10, padding: '2px 8px' }}>
                              {t}
                            </span>
                          ))}
                        </div>
                      </div>
                    );
                  })}
                </div>
              )}
            </main>
          </div>
        </div>

        <div style={{ borderTop: '1px solid rgba(148, 163, 184, 0.08)', padding: '24px', textAlign: 'center' }}>
          <div className="mono-font" style={{ fontSize: 11, color: '#475569', letterSpacing: '0.25em', marginBottom: 6 }}>
            DYNASTY HUB
          </div>
          <div style={{ fontSize: 11, color: '#334155', fontWeight: 400 }}>
            Created by <span style={{ color: '#64748b', fontWeight: 500 }}>Taylor Burnett</span>
          </div>
        </div>
      </div>

      {/* Modal */}
      {showAdd && (
        <div className="modal-bg" onClick={closeForm}>
          <div className="modal" onClick={(e) => e.stopPropagation()}>
            <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: 24 }}>
              <h2 className="display-font" style={{ fontSize: 30, margin: 0, fontWeight: 600, color: '#f8fafc' }}>
                {editing ? 'Edit link' : 'New link'}
              </h2>
              <button className="icon-btn" onClick={closeForm}><X size={20} /></button>
            </div>

            <div style={{ marginBottom: 16 }}>
              <label className="label">Title</label>
              <input
                className="field"
                autoFocus
                placeholder="e.g. Q4 Leaderboard Dashboard"
                value={form.title}
                onChange={(e) => setForm({ ...form, title: e.target.value })}
              />
            </div>

            <div style={{ marginBottom: 16 }}>
              <label className="label">URL</label>
              <input
                className="field mono-font"
                style={{ fontSize: 13 }}
                placeholder="https://your-app.vercel.app"
                value={form.url}
                onChange={(e) => setForm({ ...form, url: e.target.value })}
              />
            </div>

            <div style={{ marginBottom: 16 }}>
              <label className="label">Category</label>
              <select
                className="field"
                value={form.category}
                onChange={(e) => setForm({ ...form, category: e.target.value })}
              >
                {categories.map(c => <option key={c.name} value={c.name}>{c.name}</option>)}
              </select>
            </div>

            <div style={{ marginBottom: 28 }}>
              <label className="label">Tags <span style={{ color: '#475569', fontWeight: 400 }}>· comma separated</span></label>
              <input
                className="field"
                placeholder="dashboard, live, q4"
                value={form.tags}
                onChange={(e) => setForm({ ...form, tags: e.target.value })}
              />
            </div>

            <div style={{ display: 'flex', gap: 10, justifyContent: 'flex-end' }}>
              <button className="btn-ghost" onClick={closeForm}>Cancel</button>
              <button className="btn-primary" onClick={saveLink} disabled={!form.title.trim() || !form.url.trim()}>
                <Check size={15} /> {editing ? 'Update' : 'Save'}
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
