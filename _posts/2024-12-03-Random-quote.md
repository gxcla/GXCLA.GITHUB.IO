---
title: GXC.LA随机语录
layout: post
category: article
description: 鸡汤语录虽简单，却能在低谷时给予力量，在迷茫中指引方向，提醒我们坚持初心、积极向上，是心灵的温柔支撑。
---

<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: #f0f8ff;
    }
    h2 {
        font-size: 2em;
        color: #2f4f4f;
    }
    .quote {
        font-size: 1.5em;
        color: #4b0082;
        margin-top: 60px;
        font-weight: bold;
        word-wrap: break-word;
        white-space: pre-wrap;  /* 让语录自动换行 */
        margin-bottom: 20px;
    }
    button {
        padding: 10px 20px;
        font-size: 1em;
        margin-top: 60px;
        background-color: #4caf50;
        color: white;
        border: none;
        cursor: pointer;
        border-radius: 5px;
    }
    button:hover {
        background-color: #45a049;
    }
    .copy-btn {
        background-color: #007bff;
        margin-top: 10px;
    }
    .copy-btn:hover {
        background-color: #0056b3;
    }
    .message {
        margin-top: 20px;
        color: green;
        font-size: 1.2em;
        visibility: hidden;
    }
</style>

<body>

    <h2>每天正能量^_^</h2>
    <div class="quote" id="quote"></div>
    <button onclick="displayQuote()">刷新语录</button>
    <button class="copy-btn" onclick="copyQuote()">拷贝语录</button>
    <div class="message" id="message">语录已复制到剪贴板！</div>

    <script>
        // 使用 var 代替 const，保证兼容性
        var quotes = [
            "成功是坚持下来的结果，放弃的人永远无法体会。",
            "只有经历地狱般的磨练，才能炼出创造天堂的力量。 — 拿破仑·希尔",
            "你能成功，源自你不轻言放弃的决心。",
            "即使脚步慢，也要继续前行，终会看到胜利的曙光。",
            "你还年轻，可以从任何地方开始，去做自己喜欢的事情。",
            "有目标的人生才有意义，奋斗是为了让自己过得更好。",
            "每一次坚持，都是对未来的一次投资。",
            "我们不怕失败，怕的是未曾努力过。",
            "比别人更快，能带来更大的成功。你可以做到！",
            "不必担心前方的路太远，你迈出第一步就已经在路上。",
            "成功是累积的小进步，永远不要低估努力的力量。",
            "做自己喜欢的事情，世界就会为你让路。",
            "一切成功，都是坚持到最后的人留下来的。",
            "生命的意义在于奋斗，而不是等待。",
            "没有任何一条路是轻松的，但只要勇敢走下去，就能看到不一样的风景。",
            "你想得到的，一定要去争取，不争取永远不会拥有。",
            "困难是人生的试金石，只有克服困难，才能实现梦想。",
            "要相信自己，世界上没有什么是不可能的。",
            "未来并不可怕，只要你有坚定的方向。",
            "成功并非一蹴而就，而是积累的过程。",
            "不经历风雨，怎能见彩虹？",
            "不要害怕变慢，只要不停止，成功一定属于你。",
            "每一天都在进步，未来的你会感谢现在拼搏的自己。",
            "命运给你怎样的考验，取决于你能承受多少压力。",
            "成功并非偶然，它是日复一日努力的结果。",
            "越是艰难的路，越能锤炼出你坚韧的意志。",
            "最难的时刻，往往是离成功最近的时刻。",
            "没有什么可以阻挡你前进的，只要你足够努力。",
            "每天进步一点点，未来的你会感谢现在的自己。",
            "无论你经历过多少困难，记住，始终不放弃才是最重要的。",
            "最伟大的成功来自最坚持不懈的努力。",
            "勇气并不意味着不害怕，而是尽管害怕，仍然选择前行。",
            "有目标的人生，是一场永不停歇的马拉松。",
            "坚信你自己，努力过后，你的梦想一定能成真。",
            "不怕别人看不起，就怕自己不够努力。",
            "所有的成就，都是经过艰辛努力之后的回报。",
            "没有谁可以轻易获得成功，背后需要付出无数努力。",
            "永远不要低估自己，可以在最艰难的时刻坚持下来。",
            "生活不是等待风暴过去，而是学会在风暴中跳舞。",
            "每一天都在进步，未来的你会感谢现在拼搏的自己。",
            "命运给你怎样的考验，取决于你能承受多少压力。",
            "成功并非偶然，它是日复一日努力的结果。",
            "越是艰难的路，越能锤炼出你坚韧的意志。",
            "最难的时刻，往往是离成功最近的时刻。",
            "没有什么能够阻挡你成功的决心。",
            "你离成功，从来就只有一步之遥。",
            "每一个成功的背后，都是无数次不被看见的付出。",
            "成功之路，从来不是一帆风顺，而是充满挑战和坚持。",
            "没有人能随随便便成功，唯有付出才会得到回报。",
            "不要放弃，只是因为一时的失败。",
            "继续前行，别让任何事打击你前进的信念。",
            "你要知道，成功的背后永远少不了那些努力和汗水。",
            "永远记住：不怕山高，就怕不敢走。",
            "失败是成功的前奏，真正的胜利是经历过失败的坚持。",
            "勇气的意义，就是在最黑暗的时候坚持走下去。",
            "决定未来的不是你的过去，而是你的决心与行动。",
            "前方的路，充满希望，但只有坚持才能到达。",
            "每一次努力，都会为你带来与众不同的收获。",
            "放弃了，就永远不会知道自己能走多远。",
            "如果你觉得自己做得不够好，那就再努力一点点。",
            "只要你愿意，你可以随时开始全新的生活。",
            "那些把梦想变成现实的人，是那些愿意为之付出的人。",
            "你可以不完美，但你必须不断进步。",
            "成功是付出代价的结果，敢于付出的才是赢家。",
            "永远不要放弃最初的梦想，耐心和坚持才是成功的法宝。",
            "大多数人并非失败，而是放弃了。",
            "每一次跌倒，都是为了下一次更好的起飞。",
            "成功的秘诀就是，永不放弃。",
            "不要轻易放弃，因为你不知道自己有多强。"
        ];

        // 修改箭头函数为普通函数
        function displayQuote() {
            var randomIndex = Math.floor(Math.random() * quotes.length);
            document.getElementById("quote").innerText = quotes[randomIndex];
        }

        function copyQuote() {
            var quoteText = document.getElementById("quote").innerText;
            var textArea = document.createElement("textarea");
            textArea.value = quoteText;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand("copy");
            document.body.removeChild(textArea);

            // 显示提示消息
            var message = document.getElementById("message");
            message.style.visibility = "visible";
            setTimeout(function() {
                message.style.visibility = "hidden";
            }, 2000);
        }

        // 页面加载时展示一条随机语录
        displayQuote();
    </script>

