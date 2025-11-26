
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>忠義國小體育六十一週年校慶路跑</title>
    <!-- 引入 Tailwind CSS (用於快速排版) -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- 引入 Babel 用於瀏覽器端解析 JSX (讓 React 可以在單一 HTML 檔中運作) -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- 自訂動畫樣式 -->
    <style>
        @keyframes fade-in-up {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in-up {
            animation: fade-in-up 0.5s ease-out forwards;
        }
        body {
            font-family: "Microsoft JhengHei", "Heiti TC", sans-serif;
        }
    </style>
</head>
<body class="bg-slate-50">
    <div id="root"></div>

    <script type="text/babel" data-type="module">
        // 透過 ESM 引入 React 和 Lucide Icons
        import React, { useState, useEffect } from 'https://esm.sh/react@18.2.0';
        import ReactDOM from 'https://esm.sh/react-dom@18.2.0/client';
        import { Map, Calendar, FileText, ChevronRight, Menu, X, Info, Phone, MapPin, Clock, Award } from 'https://esm.sh/lucide-react@0.263.1';

        // ==========================================
        // 🔧 使用者設定區 (由此處開始修改)
        // ==========================================
        const eventConfig = {
            // 1. 活動基本資訊
            info: {
                title: "忠義國小體育六十一週年校慶路跑",
                subtitle: "奔跑吧！忠義！傳承六十一載的活力",
                date: "2025年 12月 05日 (星期五)",
                time: "上午 08:00 - 10:00",
                location: "忠義國小操場及周邊道路",
                contactPhone: "07-7812858#130-132學務處",
            },

            // 2. 核心三大連結
            mainLinks: {
                routeMap: {
                    title: "路線圖",
                    description: "請點擊下方按鈕，查看各年級詳細路跑動線",
                    icon: "map",
                    links: [
                        { label: "二年級", url: "https://www.google.com/maps/d/u/0/edit?mid=1fmcUlhBUJ5uywAKzC7UpuytrikTXCns&usp=sharing" },
                        { label: "中年級", url: "https://www.google.com/maps/d/u/0/edit?mid=1sRNgK5BhfLThBOoCCUQSCroDAoy68Bk&usp=sharing" },
                        { label: "高年級", url: "https://www.google.com/maps/d/u/0/edit?mid=1NppSf1AjKvlmx9UjPko4bh98YtvDngY&usp=sharing" }
                    ]
                },
                schedule: {
                    title: "賽程表",
                    description: "各年級檢錄時間、起跑時間總覽",
                    url: "https://drive.google.com/file/d/173_DP54q64_qNbZ-Vn8AY0MIXC6xbPwT/view?usp=sharing",
                    icon: "calendar"
                },
                guidelines: {
                    title: "活動須知",
                    description: "參賽規則、安全注意事項與衣著規定",
                    url: "https://gemini.google.com/share/5537fdba708e",
                    icon: "file"
                }
            },

            // 3. 最新公告
            news: [
                { id: 4, date: "2025/12/06", title: "比賽結果區", url: "#" }, 
            ],

            // 4. 活動亮點
            highlights: [
                { title: "健康樂活", desc: "透過路跑活動，培養學生運動習慣與強健體魄。" },
                { title: "完賽獎勵", desc: "二到六年級男女生組各取前三名。完賽同學頒發完賽證明。" }
            ]
        };

        // ==========================================
        // 🛑 主程式與版型區
        // ==========================================
        const App = () => {
            const [isMenuOpen, setIsMenuOpen] = useState(false);
            const [scrolled, setScrolled] = useState(false);

            useEffect(() => {
                const handleScroll = () => {
                    setScrolled(window.scrollY > 50);
                };
                window.addEventListener('scroll', handleScroll);
                return () => window.removeEventListener('scroll', handleScroll);
            }, []);

            const toggleMenu = () => setIsMenuOpen(!isMenuOpen);

            const getIcon = (iconName) => {
                switch (iconName) {
                    case 'map': return <Map className="w-8 h-8" />;
                    case 'calendar': return <Calendar className="w-8 h-8" />;
                    case 'file': return <FileText className="w-8 h-8" />;
                    default: return <Info className="w-8 h-8" />;
                }
            };

            return (
                <div className="min-h-screen bg-slate-50 font-sans text-slate-800">
                    {/* Navigation */}
                    <nav className={`fixed w-full z-50 transition-all duration-300 ${scrolled ? 'bg-white shadow-md py-2' : 'bg-transparent py-4'}`}>
                        <div className="container mx-auto px-4 flex justify-between items-center">
                            <div className="flex items-center space-x-2">
                                <div className="w-10 h-10 bg-orange-500 rounded-full flex items-center justify-center text-white font-bold text-xl">
                                    忠
                                </div>
                                <span className={`text-xl font-bold tracking-wider ${scrolled ? 'text-slate-800' : 'text-white'}`}>
                                    忠義國小
                                </span>
                            </div>
                            
                            <div className="hidden md:flex space-x-8 font-medium bg-white/10 backdrop-blur-md px-6 py-2 rounded-full md:bg-transparent md:px-0 md:backdrop-blur-none">
                                <a href="#about" className={`hover:text-orange-500 transition-colors ${scrolled ? 'text-slate-600' : 'text-white'}`}>活動介紹</a>
                                <a href="#links" className={`hover:text-orange-500 transition-colors ${scrolled ? 'text-slate-600' : 'text-white'}`}>重要資訊</a>
                                <a href="#news" className={`hover:text-orange-500 transition-colors ${scrolled ? 'text-slate-600' : 'text-white'}`}>最新公告</a>
                                <a href="#contact" className={`hover:text-orange-500 transition-colors ${scrolled ? 'text-slate-600' : 'text-white'}`}>聯絡我們</a>
                            </div>

                            <button className="md:hidden text-orange-500" onClick={toggleMenu}>
                                {isMenuOpen ? <X size={28} /> : <Menu size={28} color={scrolled ? '#333' : '#fff'} />}
                            </button>
                        </div>

                        {/* Mobile Dropdown */}
                        {isMenuOpen && (
                            <div className="md:hidden bg-white absolute top-full left-0 w-full shadow-lg border-t">
                                <div className="flex flex-col p-4 space-y-4 text-center font-medium text-slate-700">
                                    <a href="#about" onClick={toggleMenu}>活動介紹</a>
                                    <a href="#links" onClick={toggleMenu}>重要資訊</a>
                                    <a href="#news" onClick={toggleMenu}>最新公告</a>
                                    <a href="#contact" onClick={toggleMenu}>聯絡我們</a>
                                </div>
                            </div>
                        )}
                    </nav>

                    {/* Hero Section */}
                    <header className="relative h-[600px] flex items-center justify-center overflow-hidden" id="about">
                        <div className="absolute inset-0 bg-gradient-to-br from-blue-900 via-blue-700 to-orange-500 z-0"></div>
                        <div className="absolute top-0 left-0 w-64 h-64 bg-white opacity-10 rounded-full -translate-x-1/2 -translate-y-1/2 blur-3xl"></div>
                        <div className="absolute bottom-0 right-0 w-96 h-96 bg-orange-400 opacity-20 rounded-full translate-x-1/3 translate-y-1/3 blur-3xl"></div>

                        <div className="relative z-10 text-center text-white px-4 max-w-4xl mx-auto mt-16">
                            <div className="inline-block px-4 py-1 mb-4 border border-orange-300 rounded-full bg-orange-500/20 text-orange-200 text-sm tracking-widest backdrop-blur-sm">
                                61ST ANNIVERSARY
                            </div>
                            <h1 className="text-4xl md:text-6xl font-black mb-6 leading-tight tracking-tight drop-shadow-lg">
                                {eventConfig.info.title}
                            </h1>
                            <p className="text-xl md:text-2xl text-blue-100 mb-8 font-light">
                                {eventConfig.info.subtitle}
                            </p>
                            
                            <div className="flex flex-col md:flex-row justify-center items-center gap-4 md:gap-8 bg-white/10 backdrop-blur-md p-4 rounded-xl border border-white/20">
                                <div className="flex items-center space-x-2">
                                    <Calendar className="text-orange-400 w-5 h-5" />
                                    <span>{eventConfig.info.date}</span>
                                </div>
                                <div className="hidden md:block w-px h-6 bg-white/30"></div>
                                <div className="flex items-center space-x-2">
                                    <Clock className="text-orange-400 w-5 h-5" />
                                    <span>{eventConfig.info.time}</span>
                                </div>
                                <div className="hidden md:block w-px h-6 bg-white/30"></div>
                                <div className="flex items-center space-x-2">
                                    <MapPin className="text-orange-400 w-5 h-5" />
                                    <span>{eventConfig.info.location}</span>
                                </div>
                            </div>
                        </div>
                    </header>
                    
                    {/* Main Links Section */}
                    <section id="links" className="py-16 -mt-20 relative z-20 px-4">
                        <div className="container mx-auto">
                            <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                                {Object.entries(eventConfig.mainLinks).map(([key, item], index) => {
                                    const cardContent = (
                                        <>
                                            <div className={`w-16 h-16 bg-orange-100 rounded-full flex items-center justify-center text-orange-600 mb-4 transition-colors duration-300 ${!item.links ? 'group-hover:bg-orange-500 group-hover:text-white' : ''}`}>
                                                {getIcon(item.icon)}
                                            </div>
                                            <h3 className="text-2xl font-bold mb-2 text-slate-800">{item.title}</h3>
                                            <p className="text-slate-500 mb-6">{item.description}</p>
                                        </>
                                    );

                                    if (item.links && item.links.length > 0) {
                                        return (
                                            <div key={key} className="bg-white rounded-2xl shadow-xl border-t-4 border-orange-500 p-8 flex flex-col items-center text-center transition-all duration-300 hover:shadow-2xl hover:-translate-y-2">
                                                {cardContent}
                                                <div className="mt-auto w-full space-y-3">
                                                    {item.links.map((link, idx) => (
                                                         <a key={idx} href={link.url} target="_blank" rel="noopener noreferrer" className="block w-full py-2.5 px-4 bg-orange-50 text-orange-600 rounded-lg hover:bg-orange-500 hover:text-white transition-all duration-200 font-bold flex items-center justify-center group">
                                                             {link.label} 
                                                             <ChevronRight className="w-4 h-4 ml-1 opacity-50 group-hover:opacity-100 group-hover:translate-x-1 transition-all" />
                                                         </a>
                                                    ))}
                                                </div>
                                            </div>
                                        );
                                    }

                                    return (
                                        <a key={key} href={item.url} target="_blank" rel="noopener noreferrer" className="group bg-white rounded-2xl shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 overflow-hidden border-t-4 border-orange-500 p-8 flex flex-col items-center text-center">
                                            {cardContent}
                                            <div className="mt-auto flex items-center text-orange-600 font-bold group-hover:text-orange-500">
                                                點擊查看 <ChevronRight className="w-4 h-4 ml-1 group-hover:translate-x-1 transition-transform" />
                                            </div>
                                        </a>
                                    );
                                })}
                            </div>
                        </div>
                    </section>

                    {/* Highlights & News */}
                    <section id="news" className="py-16 bg-white">
                        <div className="container mx-auto px-4">
                            <div className="flex flex-col lg:flex-row gap-12">
                                <div className="lg:w-3/5">
                                    <div className="flex items-center mb-6">
                                        <Award className="text-orange-500 mr-2" />
                                        <h2 className="text-3xl font-bold text-slate-800">活動特色</h2>
                                    </div>
                                    <div className="grid grid-cols-1 sm:grid-cols-2 gap-6">
                                        {eventConfig.highlights.map((highlight, idx) => (
                                            <div key={idx} className="bg-slate-50 p-6 rounded-xl border border-slate-100">
                                                <h3 className="text-xl font-bold text-blue-900 mb-2">{highlight.title}</h3>
                                                <p className="text-slate-600 leading-relaxed">{highlight.desc}</p>
                                            </div>
                                        ))}
                                    </div>
                                </div>

                                <div className="lg:w-2/5">
                                   <div className="flex items-center mb-6">
                                        <Info className="text-orange-500 mr-2" />
                                        <h2 className="text-3xl font-bold text-slate-800">最新公告</h2>
                                    </div>
                                    <div className="bg-white rounded-xl shadow-sm border border-slate-200 divide-y divide-slate-100">
                                        {eventConfig.news.map((item) => (
                                            <div key={item.id} className="p-4 hover:bg-slate-50 transition-colors">
                                                <div className="flex items-center justify-between mb-1">
                                                    <span className={`text-sm font-semibold px-2 py-0.5 rounded ${item.url ? 'bg-red-50 text-red-500' : 'bg-orange-50 text-orange-500'}`}>
                                                        {item.url ? 'HOT' : 'NEWS'}
                                                    </span>
                                                    <span className="text-xs text-slate-400">{item.date}</span>
                                                </div>
                                                {item.url ? (
                                                    <a href={item.url} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:text-blue-800 hover:underline font-bold flex items-center mt-1">
                                                        {item.title} <ChevronRight className="w-4 h-4 ml-1" />
                                                    </a>
                                                ) : (
                                                    <p className="text-slate-700 font-medium mt-1">{item.title}</p>
                                                )}
                                            </div>
                                        ))}
                                    </div>
                                </div>
                            </div>
                        </div>
                    </section>

                    {/* Footer */}
                    <footer id="contact" className="bg-slate-900 text-slate-300 py-12">
                        <div className="container mx-auto px-4 text-center">
                            <div className="mb-8">
                                <h2 className="text-2xl font-bold text-white mb-2">忠義國小</h2>
                                <p className="text-slate-400">Zhong Yi Elementary School</p>
                            </div>
                            <div className="flex flex-col md:flex-row justify-center items-center gap-6 mb-8">
                                 <div className="flex items-center">
                                     <Phone className="w-5 h-5 mr-2 text-orange-500" />
                                     <span>{eventConfig.info.contactPhone}</span>
                                 </div>
                                 <div className="flex items-center">
                                     <MapPin className="w-5 h-5 mr-2 text-orange-500" />
                                     <span>{eventConfig.info.location}</span>
                                 </div>
                            </div>
                            <div className="border-t border-slate-800 pt-8 text-sm text-slate-500">
                                <p>&copy; {new Date().getFullYear()} 忠義國小體育六十一週年校慶. All rights reserved.</p>
                            </div>
                        </div>
                    </footer>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
