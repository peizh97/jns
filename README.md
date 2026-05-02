<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>岚·五色人格测试 | Arashi Personality Test</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none; /* 避免拖动/选中文本，提升卡片感，但不影响输入 */
        }

        body {
            background: linear-gradient(145deg, #f5f0e7 0%, #e8e0d5 100%);
            font-family: 'Segoe UI', 'Noto Sans JP', 'Helvetica Neue', 'PingFang SC', Roboto, system-ui, -apple-system, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1.5rem;
        }

        /* 主卡片 */
        .test-container {
            max-width: 750px;
            width: 100%;
            background: rgba(255, 255, 255, 0.96);
            border-radius: 2.5rem;
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.35), 0 4px 12px rgba(0, 0, 0, 0.05);
            overflow: hidden;
            backdrop-filter: blur(0px);
            transition: all 0.2s ease;
        }

        /* 头部 */
        .test-header {
            background: #2c2b28;
            padding: 1.6rem 2rem;
            text-align: center;
            color: #f2ede4;
        }

        .test-header h1 {
            font-size: 1.9rem;
            letter-spacing: 2px;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        .test-header h1 span {
            background: #f5f0e7;
            color: #2c2b28;
            font-size: 1.2rem;
            padding: 0.2rem 0.8rem;
            border-radius: 60px;
            font-weight: 500;
        }

        .sub {
            font-size: 0.85rem;
            opacity: 0.8;
            margin-top: 8px;
        }

        /* 进度条区域 */
        .progress-area {
            padding: 1rem 2rem 0rem 2rem;
            background: white;
        }

        .progress-info {
            display: flex;
            justify-content: space-between;
            font-size: 0.8rem;
            font-weight: 500;
            color: #5b4b3a;
            margin-bottom: 8px;
        }

        .progress-bar-bg {
            background: #e4dbd0;
            border-radius: 40px;
            height: 8px;
            overflow: hidden;
        }

        .progress-fill {
            background: #c0a080;
            width: 0%;
            height: 100%;
            border-radius: 40px;
            transition: width 0.25s ease;
            background: linear-gradient(90deg, #b38b5e, #d9b48b);
        }

        /* 题目卡片主体 */
        .question-card {
            padding: 1.8rem 2rem 2rem 2rem;
        }

        .question-text {
            font-size: 1.55rem;
            font-weight: 600;
            line-height: 1.35;
            color: #2c2b28;
            margin-bottom: 2rem;
            border-left: 5px solid #c0a080;
            padding-left: 1.2rem;
        }

        /* 选项列表 */
        .options-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-bottom: 2.5rem;
        }

        .option-item {
            background: #fefaf5;
            border: 1.5px solid #e9dfd3;
            border-radius: 2rem;
            padding: 0.9rem 1.4rem;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 1px 2px rgba(0,0,0,0.02);
        }

        .option-item:hover {
            background: #fff5ea;
            border-color: #c6ab8c;
            transform: translateX(3px);
        }

        input[type="radio"] {
            appearance: none;
            width: 20px;
            height: 20px;
            border: 2px solid #bb9e7e;
            border-radius: 50%;
            margin-right: 1rem;
            position: relative;
            cursor: pointer;
            background: white;
            transition: 0.1s;
        }

        input[type="radio"]:checked {
            background-color: #8b694a;
            border-color: #8b694a;
            box-shadow: inset 0 0 0 4px white;
        }

        .option-label {
            font-size: 1rem;
            font-weight: 500;
            color: #3a2e24;
            line-height: 1.4;
            flex: 1;
            cursor: pointer;
        }

        /* 导航按钮 */
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            gap: 1rem;
            margin-top: 0.8rem;
        }

        button {
            background: #e2d5c8;
            border: none;
            font-size: 1rem;
            font-weight: 600;
            padding: 0.8rem 1.4rem;
            border-radius: 3rem;
            cursor: pointer;
            transition: 0.2s;
            color: #2c2b28;
            font-family: inherit;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
        }

        button.primary {
            background: #8b694a;
            color: white;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        button.primary:hover {
            background: #6f4e32;
            transform: scale(0.98);
        }

        button:active {
            transform: scale(0.96);
        }

        button:hover:not(.primary) {
            background: #cebcab;
        }

        /* 结果卡片 */
        .result-overlay {
            margin: 1rem 2rem 2rem 2rem;
            background: #fef6e8;
            border-radius: 2rem;
            padding: 1.6rem;
            text-align: center;
            border: 1px solid #eedbc8;
            box-shadow: 0 8px 20px rgba(0,0,0,0.08);
            animation: fadeSlideUp 0.4s ease;
        }

        .result-member {
            font-size: 2.2rem;
            font-weight: 800;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            background: white;
            padding: 0.5rem 1.6rem;
            border-radius: 60px;
            margin-bottom: 1rem;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
        }

        .result-desc {
            color: #3e2e22;
            line-height: 1.5;
            font-size: 1rem;
            margin: 0.8rem 0;
        }

        .reset-btn {
            background: #2c2b28;
            color: white;
            margin-top: 1rem;
            padding: 0.6rem 1.8rem;
        }

        @keyframes fadeSlideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        footer {
            text-align: center;
            font-size: 0.7rem;
            color: #b9aa99;
            padding: 1.2rem 2rem 1.5rem;
            border-top: 1px solid #ede3d8;
            margin-top: 0.5rem;
        }

        @media (max-width: 550px) {
            .question-text {
                font-size: 1.3rem;
            }
            .option-label {
                font-size: 0.9rem;
            }
            .test-header h1 {
                font-size: 1.4rem;
            }
            .question-card {
                padding: 1.5rem;
            }
            button {
                padding: 0.6rem 1rem;
            }
        }

        .warning-tip {
            color: #bc6f2c;
            font-size: 0.75rem;
            margin-top: 12px;
            text-align: center;
        }
    </style >
</头>
<身体>
<差异班级="测试容器" 身份证明（identification）="应用程序">
    <差异班级="测试标题">
        <氕>
            🎌 岚·五色人格
            <跨度>岚试验</跨度>
        </氕>
        <差异班级=“子”>哪一位成员的性格镜像，藏在你的灵魂深处？</差异>
    </差异>
    <差异班级="进度区域">
        <差异班级="进度信息">
            <跨度>✨ 探索你的岚之魂</跨度>
            <跨度身份证明（identification）="问题计数器">第1 / 25题</跨度>
        </差异>
        <差异班级="进度条-背景">
            <差异班级="进度-填充" 身份证明（identification）=" progressFill "></差异>
        </差异>
    </差异>
    <差异班级=“问题卡” 身份证明（identification）=“问题卡”>
        <差异班级="问题-文本" 身份证明（identification）="问题文本">加载中...</差异>
        <差异班级="选项-列表" 身份证明（identification）="选项列表"></差异>
        <差异班级="导航按钮">
            <按钮身份证明（identification）=" prevBtn " 班级="次要">◀ 上一题</按钮>
            <按钮身份证明（identification）="下一个Btn " 班级="主要" 身份证明（identification）="下一步行动">下一题 ▶</按钮>
        </div>
        <div id="warningMsg" class="warning-tip"></div>
    </div>
    <div id="resultArea"></div>
    <footer>💙 松弛蓄力 · ❤️ 精英自律 · 💚 太阳真诚 · 💛 懒腰天才 · 💜 完美匠心</footer>
</div>

<script>
    // ---------- 根据文本描述，构建25道高区分度题目 (选项映射至五位成员) ----------
    // memberKey: 'ohno'💙 , 'sakurai'❤️ , 'aiba'💚 , 'ninomiya'💛 , 'matsujun'💜
    const QUESTIONS = [
        { text: "面对重要任务或截止日期时，你通常的状态是？", options: [
            { text: "看起来从容放松，甚至有点“佛系”，但心里有底，最后关头爆发惊人效率。", key: "ohno" },
            { text: "提前列好计划，逐项攻克，做足功课才能安心，习惯性压榨时间做到完美。", key: "sakurai" },
            { text: "用满满元气感染团队，哪怕自己疲惫也会笑着冲在前面，把压力藏起来。", key: "aiba" },
            { text: "表面上说“好麻烦”，但私下默默搞定一切，结果总是很厉害，不让人看到努力。", key: "ninomiya" },
            { text: "严格拆分步骤，反复推敲每一个细节，不做到极致绝不罢休，对自己高标准。", key: "matsujun" }
        ]},
        { text: "在团队合作中，你更倾向于扮演什么角色？", options: [
            { text: "安静的定海神针，平时不主导，但关键时刻稳定军心，大家都依赖你的存在。", key: "ohno" },
            { text: "逻辑梳理者，负责整理信息、把控流程，保证一切有序进行。", key: "sakurai" },
            { text: "气氛制造者，主动照顾每个人情绪，用真诚让团队凝聚在一起。", key: "aiba" },
            { text: "万能辅助，什么都会一点，灵活切换角色，总能出奇制胜。", key: "ninomiya" },
            { text: "执行总控，从构思到落地严格把关，把每个环节打磨到极致。", key: "matsujun" }
        ]},
        { text: "你喜欢的休闲方式更像哪一种？", options: [
            { text: "独处时光：钓鱼、画画、做手工，享受安静蓄能的节奏。", key: "ohno" },
            { text: "吸收新知：看新闻、钻研感兴趣领域，充实大脑。", key: "sakurai" },
            { text: "户外撒欢或和朋友一起大笑，单纯直接的快乐。", key: "aiba" },
            { text: "打游戏、变魔术、钻研小众技能，兴趣广泛又很会玩。", key: "ninomiya" },
            { text: "研究某个爱好到专业级别，比如摄影、设计或者健身细节。", key: "matsujun" }
        ]},
        { text: "朋友评价你的性格特质，最可能的是？", options: [
            { text: "看似懒洋洋，其实很通透，有自己独特节奏，不争不抢却很有才华。", key: "ohno" },
            { text: "靠谱精英，做事认真负责，但私下也有反差萌可爱一面。", key: "sakurai" },
            { text: "天然纯粹，像小太阳一样温暖，永远真诚待人，不设防。", key: "aiba" },
            { text: "聪明机灵，吐槽精准，看起来嫌麻烦但其实内心细腻。", key: "ninomiya" },
            { text: "严格又温柔，追求完美但默默照顾别人，不擅口头表达。", key: "matsujun" }
        ]},
        { text: "遇到挫折或情绪低谷时，你的应对方式是？", options: [
            { text: "给自己放空的时间，钓鱼画画转移注意，恢复后自然解决。", key: "ohno" },
            { text: "分析问题根源，大量查阅资料，用理性与努力跨过难关。", key: "sakurai" },
            { text: "即使难受也先笑给周围人看，用行动治愈自己和大家。", key: "aiba" },
            { text: "用吐槽调侃掩盖低落，私下自己消化，不愿暴露脆弱。", key: "ninomiya" },
            { text: "默默改进自己，把挫折变成更严格的标准，不断打磨。", key: "matsujun" }
        ]},
        { text: "对于「努力」这件事，你的态度是？", options: [
            { text: "努力不需要给别人看，蓄力是为了精准爆发，平时轻松点挺好。", key: "ohno" },
            { text: "努力是日常习惯，哪怕枯燥也会坚持，相信积累的力量。", key: "sakurai" },
            { text: "拼命是理所当然，为了在乎的人，可以燃烧自己照亮大家。", key: "aiba" },
            { text: "不喜欢宣扬努力，总是一副“随便做做就很强”的样子，其实私下很拼。", key: "ninomiya" },
            { text: "努力到极致才安心，不放过任何瑕疵，是责任感驱使。", key: "matsujun" }
        ]},
        { text: "在聚会上或热闹场合，你通常会？", options: [
            { text: "待在角落观察，必要时才开口，但并不冷漠。", key: "ohno" },
            { text: "把控节奏，照顾到每个人，偶尔喝嗨了会放飞自我。", key: "sakurai" },
            { text: "最放得开，不怕出丑，成为大家的开心果。", key: "aiba" },
            { text: "见招拆招，接梗达人，懒洋洋却总是妙语连珠。", key: "ninomiya" },
            { text: "默默安排细节，确保场地、气氛到位，低调可靠。", key: "matsujun" }
        ]},
        { text: "关于创意或艺术创作，你觉得自己？", options: [
            { text: "天生有灵感，绘画或创作信手拈来，但从不炫耀。", key: "ohno" },
            { text: "愿意学习幕后构成，用逻辑和知识去策划创意。", key: "sakurai" },
            { text: "用直觉和真诚表达，作品总是充满温暖与生命力。", key: "aiba" },
            { text: "全能型，模仿、作曲、演戏都擅长，举重若轻。", key: "ninomiya" },
            { text: "细节控，对色彩、灯光、布局都有严苛要求，追求完美视觉。", key: "matsujun" }
        ]},
        { text: "团队出现混乱或意见分歧，你会？", options: [
            { text: "安静但关键的一句话点醒大家，不做主导却稳住局面。", key: "ohno" },
            { text: "快速梳理信息，给出理性方案，用数据或逻辑说服。", key: "sakurai" },
            { text: "先安抚情绪，用真诚和笑容化解矛盾，照顾每个人感受。", key: "aiba" },
            { text: "用吐槽或机智化解紧张，然后提出折中方案。", key: "ninomiya" },
            { text: "提出具体执行标准，带头落实，用行动统一意见。", key: "matsujun" }
        ]},
        { text: "别人给你贴标签，你更希望是？", options: [
            { text: "深藏不露的艺术家，松弛又有力量。", key: "ohno" },
            { text: "值得信赖的精英，可靠且多面。", key: "sakurai" },
            { text: "真诚的治愈者，永远给人带来笑容。", key: "aiba" },
            { text: "天才般的机灵鬼，什么都能搞定。", key: "ninomiya" },
            { text: "追求极致的匠人，温柔又严格。", key: "matsujun" }
        ]},
        { text: "工作或学习中，你更在意？", options: [
            { text: "内在的创作自由与舒适节奏，而不是外界评价。", key: "ohno" },
            { text: "知识的积累与逻辑的严谨，结果要对得起付出。", key: "sakurai" },
            { text: "团队的氛围与大家的笑容，过程开心很重要。", key: "aiba" },
            { text: "效率与巧妙的方法，能用最短时间做到最好。", key: "ninomiya" },
            { text: "每个细节的品质，不容许有瑕疵。", key: "matsujun" }
        ]},
        { text: "你理想中的团队伙伴，你更欣赏哪种？", options: [
            { text: "平时安静但才华惊人的类型。", key: "ohno" },
            { text: "努力又有条理，能一起进步的同伴。", key: "sakurai" },
            { text: "热情真诚，愿意为团队付出的人。", key: "aiba" },
            { text: "聪明灵活，幽默感十足的多面手。", key: "ninomiya" },
            { text: "严谨负责，能把事情做到120%的人。", key: "matsujun" }
        ]},
        { text: "对待陌生挑战，你的第一反应是？", options: [
            { text: "看起来没兴趣，但内心已经在蓄力，准备一鸣惊人。", key: "ohno" },
            { text: "立刻开始收集资料，系统学习，不惧怕任何硬骨头。", key: "sakurai" },
            { text: "先笑着冲上去试试，就算失败也不怕。", key: "aiba" },
            { text: "嘴上说麻烦，背地里偷偷研究，然后惊艳所有人。", key: "ninomiya" },
            { text: "制定完美计划，反复演练直到万无一失。", key: "matsujun" }
        ]},
        { text: "朋友心情低落找你倾诉，你更可能？", options: [
            { text: "安静倾听，简单安慰，用陪伴代替言语。", key: "ohno" },
            { text: "给出理性分析和建议，帮助整理思绪。", key: "sakurai" },
            { text: "带他吃好吃的、玩开心，用笑容感染对方。", key: "aiba" },
            { text: "用幽默化解沉重，但内心记得对方的难过。", key: "ninomiya" },
            { text: "默默记住对方的习惯，之后悄悄送药或关心行动。", key: "matsujun" }
        ]},
        { text: "面对需要大量准备的工作，你？", options: [
            { text: "前期松弛，后期集中火力高效完成。", key: "ohno" },
            { text: "早早开始，系统化准备，杜绝任何意外。", key: "sakurai" },
            { text: "用热情感染他人，一起加油冲过去。", key: "aiba" },
            { text: "看起来游刃有余，实际上已经把所有功课做完了。", key: "ninomiya" },
            { text: "画出详细流程图，反复校对每个步骤。", key: "matsujun" }
        ]},
        { text: "你给人的第一印象往往是什么？", options: [
            { text: "慢半拍、有点冷淡，但熟悉后会发现很有趣。", key: "ohno" },
            { text: "精英感、知性可靠，稍微有点距离感。", key: "sakurai" },
            { text: "开朗阳光，毫无攻击性，天然呆萌。", key: "aiba" },
            { text: "少年感，说话懒懒的，但很聪明。", key: "ninomiya" },
            { text: "认真严肃、气场强大，但其实很温柔。", key: "matsujun" }
        ]},
        { text: "你对「完美主义」的看法是？", options: [
            { text: "更追求本质的完美，不纠结形式，自然就好。", key: "ohno" },
            { text: "完美来自充分准备和逻辑闭环。", key: "sakurai" },
            { text: "不追求完美，更希望所有人都开心。", key: "aiba" },
            { text: "心里有完美标准，但懒得表现出来。", key: "ninomiya" },
            { text: "完美是基本要求，必须付出全部努力。", key: "matsujun" }
        ]},
        { text: "如果被分到大型活动的幕后策划，你会负责？", options: [
            { text: "创意核心，但不喜欢繁琐管理，灵感爆发。", key: "ohno" },
            { text: "总构架与流程，确保每个环节衔接顺畅。", key: "sakurai" },
            { text: "后勤和气氛组，让大家不累又开心。", key: "aiba" },
            { text: "万能替补，哪里缺人补哪里，且做得很好。", key: "ninomiya" },
            { text: "灯光、舞台、细节落地，每个角度都要完美。", key: "matsujun" }
        ]},
        { text: "你更擅长哪种沟通风格？", options: [
            { text: "少说多做，关键时刻一句到位。", key: "ohno" },
            { text: "逻辑清晰，信息整合，让人信服。", key: "sakurai" },
            { text: "真诚直接，从不拐弯抹角，充满善意。", key: "aiba" },
            { text: "机智调侃，让人又爱又恨但离不开。", key: "ninomiya" },
            { text: "行动派沟通，默默把事情做好来表达关心。", key: "matsujun" }
        ]},
        { text: "关于「野心」，你的态度是？", options: [
            { text: "藏在松弛表象下，有自己的坚持和目标，但不张扬。", key: "ohno" },
            { text: "会明确规划并一步步实现，努力是野心的翅膀。", key: "sakurai" },
            { text: "野心是让身边人幸福，为此可以付出一切。", key: "aiba" },
            { text: "不喜欢谈论野心，但内心很清楚自己要什么。", key: "ninomiya" },
            { text: "野心是每个细节都要做到最好，不辜负期待。", key: "matsujun" }
        ]},
        { text: "你觉得自己的性格更接近哪种动物？", options: [
            { text: "猫：独立安静，慵懒但敏锐。", key: "ohno" },
            { text: "狼：严谨，有团队意识，坚韧。", key: "sakurai" },
            { text: "金毛犬：温暖忠诚，永远充满活力。", key: "aiba" },
            { text: "狐狸：聪明，灵活，有点小狡猾。", key: "ninomiya" },
            { text: "猎豹：目标精准，追求极致速度与完美。", key: "matsujun" }
        ]},
        { text: "别人形容你「举重若轻」，你会觉得？", options: [
            { text: "那正是我的理想状态，内心有数，外表从容。", key: "ohno" },
            { text: "那是因为背后的努力没被看到。", key: "sakurai" },
            { text: "希望把压力藏起来，让别人轻松。", key: "aiba" },
            { text: "哈，被发现了？其实我也很认真啦。", key: "ninomiya" },
            { text: "做得不够好才需要更努力，还不够举重若轻。", key: "matsujun" }
        ]},
        { text: "如果你能拥有一项超能力，希望是？", options: [
            { text: "随时进入心流状态，创作爆发。", key: "ohno" },
            { text: "过目不忘，学什么都快。", key: "sakurai" },
            { text: "治愈光环，让周围人永远开心。", key: "aiba" },
            { text: "万能模仿，任何技能立刻学会。", key: "ninomiya" },
            { text: "时间控制，能把细节打磨到无限完美。", key: "matsujun" }
        ]},
        { text: "在恋爱或友情中，你更倾向于？", options: [
            { text: "默默陪伴，不擅长甜言，但行动踏实。", key: "ohno" },
            { text: "照顾对方生活学习，用计划给安全感。", key: "sakurai" },
            { text: "不断制造快乐，让对方感受阳光。", key: "aiba" },
            { text: "嘴上吐槽，但私下记得所有小细节。", key: "ninomiya" },
            { text: "在对方需要之前就把事情做好，很笨拙但真诚。", key: "matsujun" }
        ]},
        { text: "最后，人生信条更符合哪一句？", options: [
            { text: "不必时刻紧绷，也可以把事情做到极致。", key: "ohno" },
            { text: "努力不是苦行，而是一种可以带着笑容坚持的日常。", key: "sakurai" },
            { text: "温柔不需要技巧，拼命不需要声张。", key: "aiba" },
            { text: "平时不显山露水，关键时刻从不掉链子。", key: "ninomiya" },
            { text: "做了十分，只说三分，行动是最好的语言。", key: "matsujun" }
        ]}
    ];

    // 成员映射详细资料
    const MEMBER_MAP = {
        ohno:   { name: "大野智", emoji: "💙", desc: "松弛蓄力，才华内敛，如定海神针般存在。你不必时刻紧绷，也能把事情做到极致，拥有惊人的专注力与创作天赋。" },
        sakurai:{ name: "樱井翔", emoji: "❤️", desc: "精英学霸，逻辑可靠，努力融入日常。你在严谨中带着人情味，能把混乱整理清晰，并带着笑容坚持向前。" },
        aiba:   { name: "相叶雅纪", emoji: "💚", desc: "太阳般真诚，温暖纯粹。你燃烧自己照亮他人，用真心治愈世界，是团队中无可替代的光。" },
        ninomiya:{ name: "二宫和也", emoji: "💛", desc: "万能天才，举重若轻。你聪明机灵，看似慵懒却深藏不漏，总在关键时刻展现惊人实力，细腻又幽默。" },
        matsujun:{ name: "松本润", emoji: "💜", desc: "完美匠人，严格而温柔。你追求极致，把责任扛在肩上，做了十分只讲三分，用行动默默守护所有人。" }
    };

    let currentIndex = 0;            // 0-index
    let answers = new Array(QUESTIONS.length).fill(null);   // 存储每道题的key
    let resultDisplayed = false;

    // DOM 元素
    const questionTextEl = document.getElementById('questionText');
    const optionsListEl = document.getElementById('optionsList');
    const prevBtn = document.getElementById('prevBtn');
    const nextBtn = document.getElementById('nextBtn');
    const questionCounterSpan = document.getElementById('questionCounter');
    const progressFill = document.getElementById('progressFill');
    const warningMsgDiv = document.getElementById('warningMsg');
    const resultArea = document.getElementById('resultArea');

    // 渲染当前题目
    function renderCurrentQuestion() {
        const q = QUESTIONS[currentIndex];
        questionTextEl.innerText = q.text;
        // 生成选项html
        let optionsHtml = '';
        q.options.forEach((opt, idx) => {
            const isChecked = (answers[currentIndex] === opt.key);
            const checkedAttr = isChecked ? 'checked' : '';
            optionsHtml += `
                <div class="option-item" data-key="${opt.key}">
                    <input type="radio" name="questionOption" id="opt_${idx}" value="${opt.key}" ${checkedAttr}>
                    <label class="option-label" for="opt_${idx}">${opt.text}</label>
                </div>
            `;
        });
        optionsListEl.innerHTML = optionsHtml;

        // 绑定点击整行选中radio事件
        document.querySelectorAll('.option-item').forEach(item => {
            const radio = item.querySelector('input[type="radio"]');
            item.addEventListener('click', (e) => {
                if (e.target.tagName !== 'INPUT') {
                    radio.checked = true;
                    // 手动触发change
                    const changeEvent = new Event('change', { bubbles: true });
                    radio.dispatchEvent(changeEvent);
                }
            });
            radio.addEventListener('change', (e) => {
                if (radio.checked) {
                    const selectedKey = radio.value;
                    answers[currentIndex] = selectedKey;
                    warningMsgDiv.innerText = ''; // 清除警告
                }
            });
        });

        // 更新计数 & 进度条
        questionCounterSpan.innerText = `第${currentIndex+1} / ${QUESTIONS.length}题`;
        const percent = ((currentIndex+1) / QUESTIONS.length) * 100;
        progressFill.style.width = `${percent}%`;

        // 控制按钮文字: 最后一题时next显示“✨ 结束 & 匹配结果”
        if (currentIndex === QUESTIONS.length - 1) {
            nextBtn.innerText = '✨ 结束 · 匹配结果 ✨';
        } else {
            nextBtn.innerText = '下一题 ▶';
        }
    }

    // 检查当前题目是否已选
    function isCurrentAnswered() {
        if (answers[currentIndex] === null || answers[currentIndex] === undefined) {
            warningMsgDiv.innerText = '💡 请选择一个选项，再继续下一题吧～';
            return false;
        }
        warningMsgDiv.innerText = '';
        return true;
    }

    // 上一题
    function goPrev() {
        if (currentIndex > 0) {
            currentIndex--;
            renderCurrentQuestion();
        } else {
            warningMsgDiv.innerText = '已经是第一题啦✨';
            setTimeout(() => { if(warningMsgDiv.innerText === '已经是第一题啦✨') warningMsgDiv.innerText = ''; }, 1000);
        }
    }

    // 下一题或提交
    function handleNextOrResult() {
        if (!isCurrentAnswered()) return;

        if (currentIndex === QUESTIONS.length - 1) {
            // 最终提交，计算匹配结果
            computeAndShowResult();
        } else {
            // 正常下一题
            currentIndex++;
            renderCurrentQuestion();
        }
    }

    // 计算匹配得分最高的成员
    function computeAndShowResult() {
        // 确保所有题目都答了 (以防万一)
        for (let i = 0; i < answers.length; i++) {
            if (answers[i] === null) {
                // 跳转到未答题
                currentIndex = i;
                renderCurrentQuestion();
                warningMsgDiv.innerText = `⚠️ 还有未完成的第${i+1}题，请先完成～`;
                return;
            }
        }

        const scoreMap = {
            ohno: 0, sakurai: 0, aiba: 0, ninomiya: 0, matsujun: 0
        };
        for (let ans of answers) {
            if (scoreMap[ans] !== undefined) scoreMap[ans]++;
        }

        // 找到最高分成员
        let maxScore = -1;
        let resultKey = 'ohno';
        for (let [key, val] of Object.entries(scoreMap)) {
            if (val > maxScore) {
                maxScore = val;
                resultKey = key;
            }
        }
        // 若出现平局(极少)，选择优先顺序按原描述：ohno,sakurai,aiba,ninomiya,matsujun
        // 但平局时取第一个最高分即可，我们上面已经记录了第一个最高分，无需额外处理。

        const member = MEMBER_MAP[resultKey];
        // 生成结果HTML，并隐藏题目卡片区域或附加在下方
        const resultHtml = `
            <div class="result-overlay" id="resultBox">
                <div class="result-member">
                    ${member.emoji} ${member.name} ${member.emoji}
                </div>
                <div class="result-desc">
                    ${member.desc}
                </div>
                <button class="reset-btn" id="resetTestBtn">🔄 重新测试</button>
            </div>
        `;
        resultArea.innerHTML = resultHtml;
        // 可选：平滑滚动到结果
        document.getElementById('resultBox')?.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
        // 禁用选项区避免修改（视觉上可选但会提醒）
        const radioGroup = document.querySelectorAll('.options-list input');
        radioGroup.forEach(r => r.disabled = true);
        warningMsgDiv.innerText = '🎉 测试完成！你的岚人格已经揭晓 🎉';
        
        // 重置按钮事件
        常数 resetBtnDom=文档。getElementById(重置测试Btn ');
        如果 (resetBtnDom) {
resetBtnDom。addEventListener(点击, () => {
                重置测试();
            });
        }
结果显示=真实的;
    }

    功能 重置测试() {
        // 重置所有答案
答案=新的排列(问题。长度).充满(空);
当前索引=0;
结果显示=错误的;
结果区域。innerHTML = '';'';'';'';
        // 启用radio (在渲染时自然启用)// 启用radio (在渲染时自然启用)// 启用radio (在渲染时自然启用)// 启用radio (在渲染时自然启用)
        renderCurrent问题();renderCurrent问题();renderCurrent问题();renderCurrent问题();
        // 清空警告
warningMsgDiv.内部人员 Text='';'';'';'';
        // 重新使能选项 (render里重新生成, 所以不需要额外)// 重新使能选项 (render里重新生成, 所以不需要额外)// 重新使能选项 (render里重新生成, 所以不需要额外)// 重新使能选项 (render里重新生成, 所以不需要额外)
        // 滚动到顶部
这个视窗 关于 关于关于ScrollTo({ 顶端: 0, 行为: “平滑” });({ 顶端: 0, 行为: “平滑” });视窗 关于 关于ScrollTo({ 顶端: 0, 行为: “平滑” });({ 顶端: 0, 行为: “平滑” });
    }

    // 事件绑定
PrevBtn。使用 使用使用 addEventListener(点击关于戈普雷夫);(点击关于戈普雷夫);使用 使用 addEventListener(点击关于戈普雷夫);(点击关于戈普雷夫);
NextBtn。使用 使用使用 addEventListener(使用handleNextOrResult);(使用handleNextOrResult);使用 使用 addEventListener(使用handleNextOrResult);(使用handleNextOrResult);

    // 初始渲染
    关于渲染当前();关于渲染当前()；关于渲染当前关于渲染当前);渲染当前问题();
</脚本>
</身体>
</超文本标记语言># jns/超文本标记语言#jns 的
