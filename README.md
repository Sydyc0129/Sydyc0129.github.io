<!DOCTYPE html>
<html lang="zh-CN" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>孙乙丁 (Yiding Sun) - AI产品与数据专家</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&family=Noto+Sans+SC:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        /* General Styles */
        body {
            font-family: 'Inter', 'Noto Sans SC', sans-serif;
            background-color: #000000;
            color: #E0E0E0;
            overflow-x: hidden;
        }
        .glow-background {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(ellipse at top, rgba(29, 78, 216, 0.15), transparent 60%),
                        radial-gradient(ellipse at bottom, rgba(79, 70, 229, 0.15), transparent 70%);
            z-index: -1;
        }
        .gradient-text {
            background: linear-gradient(90deg, #A78BFA, #F472B6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .section-card {
            background-color: rgba(17, 24, 39, 0.5); border: 1px solid rgba(55, 65, 81, 0.5);
            backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }
        .section-card:hover {
            border-color: rgba(167, 139, 250, 0.7); transform: translateY(-5px);
        }
        .skill-tag {
            background-color: rgba(55, 65, 81, 0.4); border: 1px solid rgba(55, 65, 81, 1);
            transition: all 0.3s ease;
        }
        .skill-tag:hover {
            background-color: rgba(79, 70, 229, 0.5); border-color: rgba(129, 140, 248, 0.8);
            color: #FFFFFF;
        }
        nav {
            background-color: rgba(0, 0, 0, 0.6); backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
        .fade-in { opacity: 0; animation: fadeInAnimation 1s ease-in forwards; }
        .scroll-fade-in { opacity: 0; transform: translateY(30px); transition: opacity 0.8s ease-out, transform 0.8s ease-out; }
        .scroll-fade-in.visible { opacity: 1; transform: translateY(0); }
        @keyframes fadeInAnimation { from { opacity: 0; } to { opacity: 1; } }

        /* AI Chatbot Styles */
        #chat-fab {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background: linear-gradient(90deg, #4f46e5, #9333ea);
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 4px 20px rgba(124, 58, 237, 0.5);
            transition: all 0.3s ease;
            z-index: 99;
        }
        #chat-fab:hover { transform: scale(1.1); box-shadow: 0 6px 25px rgba(124, 58, 237, 0.7); }

        #chat-widget {
            position: fixed;
            bottom: 7rem;
            right: 2rem;
            width: 90%;
            max-width: 400px;
            height: 500px;
            background-color: rgba(17, 24, 39, 0.8);
            border: 1px solid rgba(55, 65, 81, 0.7);
            backdrop-filter: blur(15px);
            border-radius: 1rem;
            display: flex;
            flex-direction: column;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            transform: translateY(20px) scale(0.95);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease-out;
            z-index: 100;
        }
        #chat-widget.visible { transform: translateY(0) scale(1); opacity: 1; visibility: visible; }
        
        .chat-header {
            padding: 1rem;
            border-bottom: 1px solid rgba(55, 65, 81, 0.7);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .chat-header h3 { font-weight: 700; color: white; }
        
        .chat-messages { flex-grow: 1; padding: 1rem; overflow-y: auto; }
        
        .message { display: flex; margin-bottom: 1rem; max-width: 90%; }
        .message-content { padding: 0.75rem; border-radius: 0.75rem; line-height: 1.5; }

        .user-message { margin-left: auto; }
        .user-message .message-content { background-color: #4f46e5; color: white; border-bottom-right-radius: 0; }

        .ai-message { margin-right: auto; }
        .ai-message .message-content { background-color: #374151; color: #e5e7eb; border-bottom-left-radius: 0; }
        .ai-message.thinking .message-content {
            display: flex;
            align-items: center;
        }
        .dot-flashing {
            position: relative; width: 5px; height: 5px; border-radius: 5px;
            background-color: #a78bfa; color: #a78bfa;
            animation: dot-flashing 1s infinite linear alternate; animation-delay: .5s;
        }
        .dot-flashing::before, .dot-flashing::after {
            content: ''; display: inline-block; position: absolute; top: 0;
        }
        .dot-flashing::before {
            left: -10px; width: 5px; height: 5px; border-radius: 5px;
            background-color: #a78bfa; color: #a78bfa;
            animation: dot-flashing 1s infinite alternate; animation-delay: 0s;
        }
        .dot-flashing::after {
            left: 10px; width: 5px; height: 5px; border-radius: 5px;
            background-color: #a78bfa; color: #a78bfa;
            animation: dot-flashing 1s infinite alternate; animation-delay: 1s;
        }
        @keyframes dot-flashing {
            0% { background-color: #a78bfa; }
            50%, 100% { background-color: rgba(167, 139, 250, 0.3); }
        }

        .chat-input { padding: 1rem; border-top: 1px solid rgba(55, 65, 81, 0.7); display: flex; gap: 0.5rem; }
        .chat-input input {
            flex-grow: 1; background-color: #1f2937; border: 1px solid #4b5563;
            color: white; border-radius: 0.5rem; padding: 0.75rem;
            transition: border-color 0.2s;
        }
        .chat-input input:focus { outline: none; border-color: #6366f1; }
        .chat-input button {
            background-color: #4f46e5; color: white; font-weight: 600;
            border: none; border-radius: 0.5rem; padding: 0 1rem;
            cursor: pointer; transition: background-color 0.2s;
        }
        .chat-input button:hover { background-color: #6366f1; }
        .chat-input button:disabled { background-color: #4b5563; cursor: not-allowed; }
    </style>
</head>
<body class="w-full">
    <div class="glow-background"></div>

    <!-- Main Content (Same as before) -->
    <header class="sticky top-0 z-50 fade-in">
        <nav class="container mx-auto px-6 py-3 border-b border-gray-800">
            <div class="flex justify-between items-center">
                <div class="text-xl font-bold text-white">孙乙丁</div>
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#about" class="text-gray-300 hover:text-white transition">关于我</a>
                    <a href="#experience" class="text-gray-300 hover:text-white transition">工作经历</a>
                    <a href="#skills" class="text-gray-300 hover:text-white transition">专业技能</a>
                    <a href="#contact" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-lg transition">联系我</a>
                </div>
                <div class="md:hidden">
                    <a href="#contact" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-lg transition text-sm">联系</a>
                </div>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-6 py-16 sm:py-24">
        <section id="hero" class="text-center min-h-[60vh] flex flex-col justify-center items-center fade-in">
            <h1 class="text-5xl md:text-7xl font-black text-white leading-tight">
                孙乙丁 <span class="text-gray-400 font-bold">Yiding Sun</span>
            </h1>
            <h2 class="mt-4 text-2xl md:text-3xl font-bold gradient-text">AI产品与数据专家</h2>
            <p class="mt-6 max-w-2xl mx-auto text-lg text-gray-300">
                我致力于通过数据驱动的策略和AI解决方案，赋能金融科技的未来，打造人机协作的新范式。
            </p>
            <div class="mt-10">
                <a href="#experience" class="bg-white text-black font-bold py-3 px-8 rounded-lg hover:bg-gray-200 transition text-lg">
                    查看我的经历
                </a>
            </div>
        </section>

        <section id="about" class="py-20 scroll-fade-in">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-12 items-center">
                <div class="md:col-span-1 flex justify-center">
                    <div class="w-48 h-48 rounded-full overflow-hidden border-4 border-indigo-500/50 shadow-lg">
                        <img src="https://placehold.co/200x200/111827/a78bfa?text=SYD" alt="孙乙丁的头像" class="w-full h-full object-cover" onerror="this.onerror=null;this.src='https://placehold.co/200x200/111827/a78bfa?text=SYD';">
                    </div>
                </div>
                <div class="md:col-span-2">
                    <h2 class="text-3xl font-bold text-white mb-4">关于我</h2>
                    <p class="text-gray-300 mb-4 leading-relaxed">
                        您好，我是孙乙丁。一名对人工智能充满热情的AI项目管理专家，在AI大模型产品运营和数字化转型方面拥有丰富经验。我专注于多模态AI数据的全流程管理，并成功领导团队交付了超过10万条的文本、图片和语音标注项目。
                    </p>
                    <p class="text-gray-300 leading-relaxed">
                        我擅长将复杂的业务需求转化为清晰的技术实现路径，并协调算法、产品和运营团队高效协作。我相信，精准的数据、优化的模型和流畅的用户体验是AI产品成功的关键。
                    </p>
                    <div class="mt-6 flex flex-wrap gap-4 text-sm">
                        <span class="bg-gray-800 text-indigo-300 px-3 py-1 rounded-full">南京审计大学 (本科)</span>
                        <span class="bg-gray-800 text-indigo-300 px-3 py-1 rounded-full">英语六级 (CET-6)</span>
                        <span class="bg-gray-800 text-indigo-300 px-3 py-1 rounded-full">计算机二级</span>
                    </div>
                </div>
            </div>
        </section>

        <section id="experience" class="py-20 scroll-fade-in">
            <h2 class="text-3xl font-bold text-white text-center mb-12">工作经历</h2>
            <div class="space-y-12">
                 <div class="section-card p-8 rounded-2xl">
                    <div class="flex justify-between items-start mb-4">
                        <div><h3 class="text-xl font-bold text-white">AI数据生产项目负责人</h3><p class="text-indigo-400">智融数科科技产业发展有限公司</p></div>
                        <span class="text-gray-400 font-mono">2024.06 - 2025.05</span>
                    </div>
                    <p class="text-gray-300 mb-6"><strong>项目:</strong> 银行智能客服与客户交互项目。通过AI技术优化交互体验与问题解决能力。</p>
                    <h4 class="font-semibold text-white mb-3">核心职责与成果:</h4>
                    <ul class="list-disc list-inside space-y-2 text-gray-300">
                        <li><strong>项目统筹管理:</strong> 主导项目，将业务需求转化为技术目标，协调多团队合作，确保项目按时交付。</li>
                        <li><strong>对话交流优化:</strong> 优化单轮及多轮对话，简单指令识别准确率超95%。</li>
                        <li><strong>RAG知识库增强:</strong> 构建并优化RAG模型知识库，提升开放性问题处理能力。</li>
                        <li><strong>多模态能力优化:</strong> 训练AI识别用户截图，实现从文字应答到图文理解的升级。</li>
                        <li><strong>用户意图识别优化:</strong> 精细化标注真实语料，反哺意图识别模型，解决意图混淆问题。</li>
                        <li><strong>领域适应专项训练:</strong> 使通用AI模型“银行化”，确保专业性与合规性。</li>
                        <li><strong>数据分析与洞察:</strong> 深入挖掘多维度数据，为产品迭代提供了精准的决策依据。</li>
                        <li><strong>模型评测体系完善:</strong> 建立科学评测机制，持续推动模型关键业务指标的优化。</li>
                        <li><strong>Prompt构造策略创新:</strong> 应用CoT、Few-shot等高级Prompt技术提升复杂任务处理能力。</li>
                    </ul>
                    <div class="mt-6 border-t border-gray-700 pt-6 grid grid-cols-1 sm:grid-cols-3 gap-6 text-center">
                        <div class="bg-gray-900/50 p-4 rounded-lg"><p class="text-2xl font-bold text-green-400">65% → 85%</p><p class="text-sm text-gray-400">问题解决率提升</p></div>
                        <div class="bg-gray-900/50 p-4 rounded-lg"><p class="text-2xl font-bold text-green-400">40%</p><p class="text-sm text-gray-400">人工咨询分流量</p></div>
                        <div class="bg-gray-900/50 p-4 rounded-lg"><p class="text-2xl font-bold text-green-400">-3分钟</p><p class="text-sm text-gray-400">复杂问题平均处理时长</p></div>
                    </div>
                </div>
                <div class="section-card p-8 rounded-2xl">
                    <div class="flex justify-between items-start mb-4">
                        <div><h3 class="text-xl font-bold text-white">数据标注师</h3><p class="text-indigo-400">360安全科技股份有限公司</p></div>
                        <span class="text-gray-400 font-mono">2023.07 - 2024.05</span>
                    </div>
                    <p class="text-gray-300 mb-6"><strong>项目:</strong> 自动化财务报表生成项目。通过机器学习和NLP技术，实现财务报表的自动化生成。</p>
                    <h4 class="font-semibold text-white mb-3">核心职责与成果:</h4>
                    <ul class="list-disc list-inside space-y-2 text-gray-300">
                        <li><strong>核心数据标注:</strong> 对各类财务凭证中的关键信息（科目、金额、日期等）进行精准标注。</li>
                        <li><strong>数据质量验收:</strong> 复核与验收标注数据，确保其准确性与一致性，对不合规数据提供反馈。</li>
                        <li><strong>文档与知识库管理:</strong> 整理并归档项目文档，维护项目知识库，确保信息易于检索共享。</li>
                    </ul>
                    <div class="mt-6 border-t border-gray-700 pt-6 grid grid-cols-1 sm:grid-cols-2 gap-6 text-center">
                        <div class="bg-gray-900/50 p-4 rounded-lg"><p class="text-2xl font-bold text-green-400">-20%</p><p class="text-sm text-gray-400">单文档平均标注时长</p></div>
                        <div class="bg-gray-900/50 p-4 rounded-lg"><p class="text-2xl font-bold text-green-400">-15%</p><p class="text-sm text-gray-400">团队重复性疑问减少</p></div>
                    </div>
                </div>
            </div>
        </section>

        <section id="skills" class="py-20 scroll-fade-in">
            <h2 class="text-3xl font-bold text-white text-center mb-12">专业技能</h2>
            <div class="flex flex-wrap justify-center gap-4 max-w-4xl mx-auto">
                <span class="skill-tag font-semibold px-5 py-2 rounded-lg">AI项目管理</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">大模型产品运营</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">多模态数据处理</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">数据标注全流程管理</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">自然语言处理 (NLP)</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">RAG知识库构建</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">Prompt Engineering</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">数据分析与洞察</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">模型评测体系</span><span class="skill-tag font-semibold px-5 py-2 rounded-lg">数字化转型</span>
            </div>
        </section>

        <section id="contact" class="py-20 text-center scroll-fade-in">
            <h2 class="text-4xl font-bold text-white">建立联系</h2>
            <p class="mt-4 max-w-xl mx-auto text-gray-300">
                我非常期待能与您交流更多关于AI、数据以及如何为您的团队创造价值的想法。
            </p>
            <div class="mt-8">
                <a href="mailto:sunyiding67@gmail.com" class="inline-block bg-indigo-600 text-white font-bold text-lg px-8 py-4 rounded-lg hover:bg-indigo-700 transition">
                    sunyiding67@gmail.com
                </a>
            </div>
             <div class="mt-8 space-y-2 text-gray-400">
                <p>电话: 17606190129</p>
                <p>户籍: 江苏徐州</p>
            </div>
        </section>
    </main>

    <footer class="border-t border-gray-800 py-8">
        <div class="container mx-auto px-6 text-center text-gray-500">
            <p>&copy; 2025 Sun Yiding. All Rights Reserved.</p>
        </div>
    </footer>

    <!-- AI Chatbot Floating Action Button -->
    <div id="chat-fab" onclick="toggleChat()">
        <!-- New, more friendly icon -->
        <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"></path>
            <path d="m12 7-1 2-2 1 2 1 1 2 1-2 2-1-2-1-1-2z"></path>
        </svg>
    </div>

    <!-- AI Chatbot Widget -->
    <div id="chat-widget">
        <div class="chat-header">
            <h3>AI 面试官</h3>
            <button onclick="toggleChat()" class="text-gray-400 hover:text-white">&times;</button>
        </div>
        <div class="chat-messages" id="chat-messages">
            <!-- Messages will be appended here -->
             <div class="message ai-message">
                <div class="message-content">你好！我是孙乙丁的AI助手。您可以向我提问任何关于他专业背景的问题，我会基于他的面试材料为您解答。</div>
            </div>
        </div>
        <div class="chat-input">
            <input type="text" id="chat-input-field" placeholder="输入您的问题..." onkeydown="handleKeydown(event)">
            <button id="chat-send-btn" onclick="sendMessage()">发送</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => { if (entry.isIntersecting) entry.target.classList.add('visible'); });
            }, { threshold: 0.1 });
            document.querySelectorAll('.scroll-fade-in').forEach(section => observer.observe(section));
        });

        // --- AI Chatbot Logic ---

        // The entire content of the provided PDF is stored here.
        const interviewPrepText = `
            面试准备文档副本

            自我介绍
            各位面试官们好, 我叫孙乙丁,来自江苏省徐州市,本科学历,毕业于南京审计大学。我拥有两年的大模型工作经验,有英语六级和计算机二级证书,上一家公司的话我是在智融数科科技发展有限公司,担任AI数据生产项目负责人一职,我的工作职责是对项目整体进行管理,推进项目进度,然后我做过的项目有智能客服,负责的项目包含1)对话交流、RAG知识库增强、多模态图片互动和领域适应专项训练、模型评测等,工作期间,管理和培训的标注团队累积超过80人,成功处理各类数据近10万条,项目的最终交付准确率长期稳定在95%以上。在团队中我也会研究各种AI工具来结合项目进行自动化办公,如利用Prompt工程生成项目所需数据、使用Cursor处理数据并提升团队效率。在深入了解贵公司的业务后,我对这个岗位充满期待,希望能有机会为贵公司做出贡献。希望我们今天可以沟通愉快!

            银行智能客服与客户交互项目项目背景
            智能客服大的项目背景:为提升银行服务效率与质量,解决传统人工客服响应慢、成本高及早期智能客服处理复杂业务能力不足等问题,开展智能客服项目。项目核心目标包括:1)对话交流优化提升基础服务效率;2)RAG知识库增强项目赋予智能体获取专业文档解答复杂开放性问题能力;3)通过多模态能力优化智能体理解并处理用户截图等图像信息的能力,实现图文协同的直观咨询。4)通过用户意图识别优化显著提升对模糊、歧义口语表达的精准理解能力;5)通过领域适应专项训练确保AI在金融专业性、合法合规上达到银行严苛标准;6)通过数据分析挖掘用户需求与模型瓶颈,为所有优化环节提供精准支撑。7)通过模型评测体系建立多维度、全场景的评估机制,为模型迭代提供客观基准;8)通过Prompt构造策略创新提升智能体在复杂场景下的深度推理能力。

            Q.银行痛点:银行面临的具体痛点是什么?
            回答:项目启动前,该合作银行正面临几个核心挑战。首先是服务量巨大且不均衡,日趋近万的用户等待咨询,高峰期客户平均时长超过60秒,导致用户满意度持续走低。其次,问题类型重复度高,我们分析历史数据,超过70%的咨询是关于账户查询、产品利率等标准化的简单问题,这占用了宝贵的人工坐席资源。最后,服务质量难以标准化,人工客服的回复口径、服务态度和专业度难以完全统一,尤其是在面对复杂情绪的客户时,容易引发客户投诉。这些具体痛点是我们项目立项的核心依据。

            Q.离职原因:那你这边为什么离职了
            回答:因为我们的业务线发展的很慢,也同时在进行项目裁员。然后虽然前公司确实给我对于那个AI项目管理的能力打下了一定的基础。但是我现在就是非常渴望能够接触到更前沿的然后一些应用场景,更广泛的一些AI产品和技术。所以我希望加入大厂这种领先团队的原因,希望能够深耕行业。然后迎接更大的挑战。

            Q.加班:这个任务就是你能够接受加班吗
            回答:和适当加班其实是可以的,就是我毕竟我还对那个AI还挺感兴趣的,一些加班项目对我自己也算是能力上的提升,所以可以接受

            Q:模型训练这一块接触的多吗?
            回答:我们进入项目是基于模型的微调的,根据需求做出相关的功能来,不是做一个大模型,而是对模型进行微调。

            Q:第一份工作,直接晋升的是管理员,还是工作一段时间才晋升?
            回答:一开始我应聘的标注岗,因为我的数据质量非常好,然后当时发展业务线的那个领导走了,然后我就被晋升成管理员了。

            Q:岗位优势:您可以说一下,您在咱们这个岗位你有哪些优势吗?
            回答:其实简历中的项目都是我优势,我在上家公司担任管理岗,有一年的管理经验,管理团队人数在15人,我做过多个项目,并通过Prompt构造、使用cursor智能体提高我的效率。

            Q:评测考察:就这一块你做评测涉及内容多吗?
            回答:模型评测的话,我们每次做完模型微调、算法训练完后,都要检验一下大模型到底有没有达到我们的标准。我们的数据集的主要来源有四个1)真实业务场景下的用户query;2)开源的测评集,比如从Hugging Face里获取; 3) prompt工程构建;4)算法提供。我们使用的评测方法是GSB对比法和评分法一起使用的混合标注策略。标注的规则维度分为通用和专项规则。为了提升数据的准确率我们对于重要的项目采用三人共同标注一条的方法。然后就是评测报告的撰写,整合信息后和算法团队商议做下一步的规划。

            Q.评测举例:你自己印象比较深刻的一个评估是哪个评估
            回答:其中我印象最深刻的,是一次针对我们的“图文识别多模态能力”的专项评测。目标是验证新能力是否能有效解决用户“无法通过发送图片咨询”的痛点。我们构建了包含真实语料和各类测试图片的评测集,并从识别准确性、响应速度、鲁棒性、合规与安全等维度进行全面考量。评测发现了模型在非标准“错误提示”截图识别能力不足和“幻觉”问题。我的解决方案是构建高质量的专项数据集进行模型微调,并将知识盲区反哺RAG知识库。我负责撰写最终的评测报告,并向需求方和算法工程师明确传达下一步的执行方案,这种高效联动是我们项目成功的关键。

            Q.准确率来源:这个准确率是由谁来定的?为什么是这个准确率?
            回答:准确率是由AI训练师和需求方一起商讨后定夺。在承接需求时,需求方会给予一个参考准确率。我们通过试标判断数据难度,权衡人效后和需求方商讨得出最终准确率。我们抽检比例大概是20%,通过这20%反推整体准确率。

            Q.准确率保障:你怎么保证自己的准确率呢?
            回答:首先,我会主导创建一份详尽的标注规范文档。其次,项目开始前,所有标注员都必须通过试标任务。项目进行中,我会定期组织“校准会议”。再次,质检过程中会监控准确率,对于规则理解问题会组织培训,对于个人问题会警示并打回数据。最后,引入三人盲标机制,取多数人一致的情况作为最终标准。

            Q.数据分析/意图拆分合并:有时候会做一些数据分析。用户的咨询热点、痛点和服务瓶颈对吧?能够举一些很具体的场景例子。
            回答:例如在对话交流优化项目中,分析发现模型经常混淆“查询转账限额”和“查询信用卡额度”这两个意图。我的解决方案是:1.拆分意图,将宽泛的“额度查询”拆分为两个更精细的意图。2.合并意图,将语料重合且逻辑相似的“查余额”、“查账单”合并为“账户查询”。3.增加负样本和边界案例。4.精细化标注与再训练。

            Q.基座模型or训练问题:如果模型回答的不好,那你们是如何分辨是基座模型的问题还是训练的问题?
            回答:我的原则是“对事不对人,用数据说话”。我会组织“三方联合复盘会”,共同随机抽取错误数据进行分析。我方(数据侧)判断标注是否有事实错误,算法侧解释模型为何做出错误判断。很多时候问题是“数据标注的颗粒度无法满足模型现阶段的需求”或出现“边缘案例”。找到根因后,共同修订标注规范并对数据返工。

            Q.印象最深用户痛点举例:您的简历上写具体用户的痛点,我想了解你有哪一个你特别印象深的用户的痛点。
            回答:在银行智能客服项目中,印象最深的是中老年用户在咨询理财产品时,因担心金融诈骗而产生的不信任感。通过分析对话日志发现这一痛点后,我主导了一系列优化工作:1.发起领域适应专项训练,让AI口吻更专业合规。2.增强RAG知识库的权威性,能引用官方文件。3.创新Prompt构造策略,让LLM扮演值得信赖的专家角色。这些措施显著改善了AI表现,提升了用户满意度。

            Q.机械性问题解决:模型有没有出现过机械性的重复回答?
            回答:我们一开始的训练时是有的,但是我们后面通过做一个项目的优化,优化的过程中就是解决这个回答的机械性重复,当时的话是因为我们数据量或者数据格式少了,让模型欠拟合了,我们当时的办法就是搭建了一个知识库,有些专业的知识必须要用知识库才能解答。

            Q.AI训练师职责:你作为项目负责人的职责?
            回答:作为AI数据生产的项目负责人,我主要负责把控整个项目的推进流程,包括需求承接、规则文档撰写优化、标注的全流程管理、项目交付、项目复盘。

            Q.管理流程:那你就可以简单说一下,你就是你管理团队的一个流程是怎样的吗
            回答:接收项目后,首先与算法或产品经理拉齐项目目标。然后撰写初步的规则文档,并找人进行试标,根据试标结果和人效估算项目周期和所需人力,并优化规则文档。之后对整个团队进行培训,开始正式标注。标注过程中会设立多个检查点进行质检。质检达标后,进行统一验收,打包数据交接给算法。

            Q.项目饱满度:那你之前带这种项目的话,一般是能够带多个吗
            回答:一般在我人手充足的情况下,并行两三个都是可以的。如果遇到紧急项目,会评估影响并与业务方沟通能否延期,或找外包公司快速处理。

            Q.标注答疑:他们应该会有很多问题就直接发群里,你这边直接答疑吗
            回答:我会让他们按照小组长收集问题,由小组长向我汇报。我会挑共性问题进行答疑,并优化规则文档。特别重要的问题会当天开会拉齐。

            Q.沟通问题:如何沟通团队表达评测过程中发现的大模型问题?
            回答:我会以文档形式清晰地指出问题、提供具体案例、分析问题类型、量化问题影响、初步归因并提出优化建议,然后与相关团队沟通。
        `;
        
        const chatWidget = document.getElementById('chat-widget');
        const chatFab = document.getElementById('chat-fab');
        const messagesContainer = document.getElementById('chat-messages');
        const inputField = document.getElementById('chat-input-field');
        const sendButton = document.getElementById('chat-send-btn');

        window.toggleChat = function() {
            chatWidget.classList.toggle('visible');
        }

        window.handleKeydown = function(event) {
            if (event.key === 'Enter') {
                sendMessage();
            }
        }

        window.sendMessage = async function() {
            const userInput = inputField.value.trim();
            if (userInput === '') return;

            // Display user message
            appendMessage(userInput, 'user');
            inputField.value = '';
            
            // Show thinking indicator
            const thinkingMessageId = `ai-msg-${Date.now()}`;
            appendMessage('...', 'ai', thinkingMessageId, true);

            // Construct prompt and call API
            const prompt = `
                你现在是孙乙丁的AI面试助手。你的任务是且只能是根据下面提供的“面试准备文档”来回答访问者（可能是招聘人员）提出的问题。

                规则：
                1. 你的所有回答【必须】完全基于以下提供的文档内容。
                2. 如果文档中明确包含了问题的答案，请以孙乙丁的口吻、专业且自信地进行回答。
                3. 如果问题的答案在文档中【找不到】，你【绝不能】使用自己的知识库进行猜测或回答。你必须礼貌地、委婉地拒绝，可以说：“感谢您的提问，不过这个问题超出了我能回答的范畴。我可以回答更多关于孙乙丁简历中提到的专业经验和项目细节，您对哪部分更感兴趣呢？”
                4. 保持回答简洁、切题。

                --- 面试准备文档开始 ---
                ${interviewPrepText}
                --- 面试准备文档结束 ---

                现在，请回答以下问题：
                ${userInput}
            `;
            
            const aiResponse = await callGemini(prompt);
            
            // Update thinking message with actual response
            const thinkingMessageElement = document.getElementById(thinkingMessageId);
            if (thinkingMessageElement) {
                thinkingMessageElement.querySelector('.message-content').innerHTML = aiResponse;
                thinkingMessageElement.classList.remove('thinking');
            }
        }

        function appendMessage(text, type, id = null, isThinking = false) {
            const messageWrapper = document.createElement('div');
            messageWrapper.className = `message ${type}-message`;
            if (id) {
                messageWrapper.id = id;
            }

            const messageContent = document.createElement('div');
            messageContent.className = 'message-content';
            
            if (isThinking) {
                messageWrapper.classList.add('thinking');
                messageContent.innerHTML = '<div class="dot-flashing"></div>';
            } else {
                messageContent.innerText = text;
            }

            messageWrapper.appendChild(messageContent);
            messagesContainer.appendChild(messageWrapper);
            messagesContainer.scrollTop = messagesContainer.scrollHeight; // Auto-scroll to bottom
        }

        // Generic Gemini API call function
        async function callGemini(prompt) {
            sendButton.disabled = true;
            inputField.disabled = true;

            const apiKey = ""; // Provided by Canvas environment
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
            
            const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                if (!response.ok) throw new Error(`API call failed: ${response.status}`);
                
                const result = await response.json();
                if (result.candidates && result.candidates.length > 0) {
                    return result.candidates[0].content.parts[0].text;
                } else {
                    return "抱歉，AI暂时无法回应，可能是由于内容安全限制。请尝试其他问题。";
                }
            } catch (error) {
                console.error("Gemini API Error:", error);
                return "调用AI服务时出错，请稍后重试。";
            } finally {
                sendButton.disabled = false;
                inputField.disabled = false;
                inputField.focus();
            }
        }
    </script>
</body>
</html>
