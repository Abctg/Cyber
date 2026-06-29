<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Case for Tenable — Cybersecurity After Mythos</title>
<style>
  :root{
    --ink:#0E1726; --ink-2:#1C2A3F; --paper:#F2EEE4; --paper-2:#E7E1D2;
    --line:#C6BCA6; --rule:#3A4861; --amber:#C8642B; --teal:#1F6F6B;
    --teal-d:#13514E; --gold:#B8893A; --crimson:#9B2D2D; --mut:#5C6677;
    --pos:#2E6B4F; --neg:#9B2D2D;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  html{scroll-behavior:smooth}
  body{background:var(--paper);color:var(--ink);
    font-family:"Iowan Old Style","Palatino Linotype",Palatino,Georgia,serif;
    line-height:1.62;-webkit-font-smoothing:antialiased}
  .mono{font-family:"SF Mono",ui-monospace,"Roboto Mono","DejaVu Sans Mono",monospace}
  .wrap{max-width:1080px;margin:0 auto;padding:0 28px}

  .mast{border-bottom:2px solid var(--ink);padding:30px 0 0;background:var(--paper)}
  .mast .top{display:flex;justify-content:space-between;align-items:flex-end;flex-wrap:wrap;gap:14px}
  .kick{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;letter-spacing:.32em;
    text-transform:uppercase;color:var(--amber);font-weight:600}
  h1.title{font-size:clamp(30px,5vw,56px);line-height:.98;letter-spacing:-.02em;
    font-weight:600;margin:10px 0 0;max-width:16ch}
  h1.title em{font-style:italic;color:var(--teal-d)}
  .author{font-family:"SF Mono",ui-monospace,monospace;font-size:11.5px;letter-spacing:.05em;
    color:var(--mut);text-align:right;text-transform:uppercase;line-height:1.7}
  .author b{color:var(--ink);display:block}

  nav.tabs{position:sticky;top:0;z-index:50;background:var(--ink);border-bottom:2px solid var(--ink)}
  nav.tabs .wrap{display:flex;overflow-x:auto;-ms-overflow-style:none;scrollbar-width:none}
  nav.tabs .wrap::-webkit-scrollbar{display:none}
  nav.tabs button{flex:0 0 auto;background:none;border:none;cursor:pointer;color:#9AA6BA;
    font-family:"SF Mono",ui-monospace,monospace;font-size:11.5px;letter-spacing:.14em;
    text-transform:uppercase;padding:15px 17px;border-bottom:3px solid transparent;transition:.18s;
    white-space:nowrap;font-weight:600;display:flex;align-items:center;gap:9px}
  nav.tabs button .n{opacity:.5;font-size:10px}
  nav.tabs button:hover{color:var(--paper)}
  nav.tabs button.active{color:var(--paper);border-bottom-color:var(--amber)}
  nav.tabs button.headline{color:#F0C99A}
  nav.tabs button.headline.active{color:#fff;border-bottom-color:#F0C99A}
  nav.tabs button:focus-visible{outline:2px solid var(--amber);outline-offset:-2px}

  .panel{display:none;animation:fade .35s ease}
  .panel.show{display:block}
  @keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
  section{padding:44px 0 52px}
  .eyebrow{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;letter-spacing:.28em;
    text-transform:uppercase;color:var(--amber);font-weight:600;display:flex;align-items:center;
    gap:12px;margin-bottom:16px}
  .eyebrow .num{color:var(--teal-d);border:1px solid var(--teal-d);border-radius:50%;width:24px;
    height:24px;display:inline-flex;align-items:center;justify-content:center;font-size:11px}
  h2{font-size:clamp(26px,3.8vw,40px);line-height:1.05;letter-spacing:-.015em;font-weight:600;
    max-width:23ch;margin-bottom:16px}
  h2 em{font-style:italic;color:var(--teal-d)}
  h3.sub{font-size:21px;letter-spacing:-.01em;margin:30px 0 12px;font-weight:600}
  p.lead{font-size:18px;color:var(--ink-2);max-width:66ch;margin-bottom:18px}
  p.body{max-width:68ch;margin-bottom:16px}
  .annot{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;color:var(--mut);
    letter-spacing:.03em;margin-top:12px}

  .shiftbox{background:var(--ink);color:var(--paper);border-radius:6px;padding:28px 26px 30px;margin-bottom:32px}
  .shift-h{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;letter-spacing:.28em;
    text-transform:uppercase;color:var(--paper-2);opacity:.7;margin-bottom:18px}
  .shiftgrid{display:grid;grid-template-columns:1fr auto 1fr;align-items:stretch}
  .col h4{font-family:"SF Mono",ui-monospace,monospace;font-size:12px;letter-spacing:.1em;
    text-transform:uppercase;margin-bottom:13px;font-weight:600}
  .col.before h4{color:#E8B98C}.col.after h4{color:#7FC9C4}
  .stack{display:flex;flex-direction:column;gap:8px}
  .layer{border:1px solid var(--rule);border-radius:3px;padding:11px 13px;font-size:14px;line-height:1.3}
  .layer .lab{font-family:"SF Mono",ui-monospace,monospace;font-size:9.5px;letter-spacing:.15em;
    text-transform:uppercase;color:#8893A6;display:block;margin-bottom:3px}
  .layer.det{border-color:#6E4326;background:rgba(200,100,43,.10)}
  .layer.det.dim{opacity:.42}
  .layer.val.hot{border-color:#3E8C86;background:rgba(31,111,107,.32)}
  .layer.val{border-color:#2C615D;background:rgba(31,111,107,.16)}
  .arrowcol{display:flex;align-items:center;justify-content:center;padding:0 18px;color:#7FC9C4}
  .arrowcol .ar{font-size:32px}
  .shift-cap{margin-top:20px;font-size:14px;color:var(--paper-2);max-width:74ch;font-style:italic;opacity:.92}
  @media(max-width:720px){.shiftgrid{grid-template-columns:1fr;gap:16px}.arrowcol .ar{transform:rotate(90deg)}}

  .stackmap{display:flex;flex-direction:column;margin:22px 0 8px;border:1px solid var(--ink);
    border-radius:5px;overflow:hidden}
  .row{display:grid;grid-template-columns:150px 1fr;background:var(--paper)}
  .row+.row{border-top:1px solid var(--line)}
  .row .tag{background:var(--ink);color:var(--paper);padding:14px;font-family:"SF Mono",ui-monospace,monospace;
    font-size:11px;letter-spacing:.1em;text-transform:uppercase;display:flex;flex-direction:column;
    justify-content:center;gap:4px}
  .row .tag b{font-size:12.5px;letter-spacing:.06em}
  .row .desc{padding:14px 18px;font-size:15px}
  .row .desc .who{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;color:var(--teal-d);
    text-transform:uppercase;margin-top:6px;display:block}
  .row.hl .tag{background:var(--teal-d)}
  @media(max-width:620px){.row{grid-template-columns:1fr}.row .tag{flex-direction:row;align-items:center;gap:10px}}

  .players{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;margin-top:22px}
  .pcard{border:1px solid var(--ink);border-radius:5px;background:var(--paper);overflow:hidden}
  .pcard.spot{border-color:var(--teal-d);border-width:2px}
  .pcard button.phead{width:100%;text-align:left;background:none;border:none;cursor:pointer;
    padding:16px 18px;display:flex;justify-content:space-between;align-items:flex-start;gap:12px;
    font-family:inherit;color:var(--ink)}
  .pcard button.phead:focus-visible{outline:2px solid var(--amber);outline-offset:-3px}
  .pcard h4{font-size:20px;letter-spacing:-.01em}
  .pcard .tick{font-family:"SF Mono",ui-monospace,monospace;font-size:10.5px;color:var(--mut);letter-spacing:.06em}
  .pcard .role{font-family:"SF Mono",ui-monospace,monospace;font-size:9.5px;letter-spacing:.13em;
    text-transform:uppercase;color:var(--amber);margin-top:8px;font-weight:600}
  .pcard.spot .role{color:var(--teal-d)}
  .pcard .chev{font-family:"SF Mono",ui-monospace,monospace;font-size:20px;color:var(--teal-d);transition:transform .25s;line-height:1}
  .pcard.open .chev{transform:rotate(45deg)}
  .pbody{max-height:0;overflow:hidden;transition:max-height .3s ease}
  .pcard.open .pbody{max-height:360px}
  .pbody .inner{padding:0 18px 16px}
  .pbody p{font-size:14px;line-height:1.5;color:var(--ink-2);margin-bottom:10px}
  .pbody .stat{display:flex;gap:18px;border-top:1px solid var(--line);padding-top:10px;flex-wrap:wrap}
  .pbody .stat div span{display:block;font-family:"SF Mono",ui-monospace,monospace;font-size:9px;
    letter-spacing:.1em;text-transform:uppercase;color:var(--mut)}
  .pbody .stat div b{font-size:16px;font-family:"SF Mono",ui-monospace,monospace}
  .pbody .stat .neg b{color:var(--neg)}
  @media(max-width:620px){.players{grid-template-columns:1fr}}

  .feature{background:var(--ink);color:var(--paper);border-radius:6px;padding:30px 28px}
  .feature .pull{font-size:clamp(19px,2.5vw,26px);line-height:1.28;font-style:italic;
    border-left:3px solid var(--amber);padding-left:20px;margin:22px 0;max-width:60ch}
  .feature p{color:var(--paper-2);max-width:64ch;margin-bottom:14px;font-size:16px}
  .gw{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--rule);border:1px solid var(--rule);
    border-radius:5px;overflow:hidden;margin-top:22px}
  .gw>div{background:var(--ink-2);padding:18px}
  .gw h5{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;letter-spacing:.15em;
    text-transform:uppercase;color:#7FC9C4;margin-bottom:8px}
  .gw p{font-size:13.5px;margin:0;color:var(--paper-2)}
  @media(max-width:620px){.gw{grid-template-columns:1fr}}

  /* TENABLE centerpiece */
  .tn-hero{background:var(--teal-d);color:var(--paper);border-radius:6px;padding:34px 30px;margin-bottom:8px}
  .tn-hero .eyebrow{color:#E8B98C}
  .tn-hero .eyebrow .num{color:var(--paper);border-color:var(--paper)}
  .tn-hero h2{color:var(--paper);max-width:22ch}
  .tn-hero h2 em{color:#F0C99A}
  .tn-hero p.lead{color:#DCE9E5;max-width:64ch}
  .tn-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:24px}
  .tn-stats .s{background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.16);border-radius:5px;padding:14px}
  .tn-stats .s span{display:block;font-family:"SF Mono",ui-monospace,monospace;font-size:9px;letter-spacing:.1em;
    text-transform:uppercase;color:#9FC6C1;margin-bottom:5px}
  .tn-stats .s b{font-size:23px;font-family:"SF Mono",ui-monospace,monospace;color:#fff;display:block;line-height:1}
  .tn-stats .s .x{font-size:11px;color:#CFE0DC;display:block;margin-top:5px;line-height:1.3}
  @media(max-width:680px){.tn-stats{grid-template-columns:1fr 1fr}}

  .pillars{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-top:26px}
  .pillar{border:1px solid var(--ink);border-radius:6px;background:var(--paper);overflow:hidden}
  .pillar .ph{background:var(--ink);color:var(--paper);padding:13px 16px;font-family:"SF Mono",ui-monospace,monospace;
    font-size:11px;letter-spacing:.12em;text-transform:uppercase;font-weight:600;display:flex;gap:10px;align-items:center}
  .pillar .ph .pn{color:#7FC9C4}
  .pillar .pc{padding:15px 16px}
  .pillar .pc h4{font-size:17px;margin-bottom:7px;letter-spacing:-.01em}
  .pillar .pc p{font-size:13.5px;color:var(--ink-2)}
  @media(max-width:760px){.pillars{grid-template-columns:1fr}}

  .moat{border:1px solid var(--ink);border-radius:6px;overflow:hidden;margin-top:18px}
  .moat .mh{display:grid;grid-template-columns:1fr 1fr;background:var(--rule)}
  .moat .mh div{padding:12px 16px;font-family:"SF Mono",ui-monospace,monospace;font-size:11px;
    letter-spacing:.1em;text-transform:uppercase;color:#fff;font-weight:600}
  .moat .mh .a{background:var(--teal-d)}.moat .mh .b{background:var(--crimson)}
  .moat .mb{display:grid;grid-template-columns:1fr 1fr}
  .moat .mb>div{padding:15px 16px;font-size:14px}
  .moat .mb .a{background:rgba(31,111,107,.07);border-right:1px solid var(--line)}
  .moat .mb .b{background:rgba(155,45,45,.05)}
  .moat .mb ul{list-style:none;margin:0;padding:0}
  .moat .mb li{padding-left:16px;position:relative;margin-bottom:8px;line-height:1.4;color:var(--ink-2)}
  .moat .mb li:before{content:"";position:absolute;left:0;top:9px;width:6px;height:6px;border-radius:50%}
  .moat .mb .a li:before{background:var(--teal-d)}
  .moat .mb .b li:before{background:var(--crimson)}
  @media(max-width:620px){.moat .mh,.moat .mb{grid-template-columns:1fr}.moat .mb .a{border-right:none;border-bottom:1px solid var(--line)}}

  .crit{display:grid;grid-template-columns:repeat(3,1fr);gap:13px;margin:24px 0 0}
  .crit div{background:var(--paper-2);border:1px solid var(--line);border-radius:5px;padding:15px}
  .crit h6{font-family:"SF Mono",ui-monospace,monospace;font-size:10px;letter-spacing:.11em;
    text-transform:uppercase;color:var(--teal-d);margin-bottom:7px}
  .crit p{font-size:13.5px;color:var(--ink-2);margin:0}
  @media(max-width:680px){.crit{grid-template-columns:1fr}}

  .scen-controls{display:flex;gap:10px;margin:22px 0 24px;flex-wrap:wrap}
  .scen-controls button{flex:1 1 160px;cursor:pointer;border:1.5px solid var(--ink);border-radius:5px;
    background:var(--paper);padding:14px;text-align:left;font-family:inherit;transition:.18s;color:var(--ink)}
  .scen-controls button:focus-visible{outline:2px solid var(--amber);outline-offset:2px}
  .scen-controls button .cl{font-family:"SF Mono",ui-monospace,monospace;font-size:10px;letter-spacing:.14em;
    text-transform:uppercase;font-weight:600;display:block;margin-bottom:5px}
  .scen-controls button .cv{font-family:"SF Mono",ui-monospace,monospace;font-size:21px;display:block}
  .scen-controls button .cd{font-size:12px;color:var(--mut);display:block;margin-top:2px}
  .scen-controls button.active[data-s="bull"]{background:var(--pos);color:#fff;border-color:var(--pos)}
  .scen-controls button.active[data-s="base"]{background:var(--ink);color:#fff;border-color:var(--ink)}
  .scen-controls button.active[data-s="bear"]{background:var(--crimson);color:#fff;border-color:var(--crimson)}
  .scen-controls button.active .cd{color:rgba(255,255,255,.75)}
  .scen-controls button.active .cl{color:rgba(255,255,255,.9)}
  .scen-panel{border:1px solid var(--ink);border-radius:6px;overflow:hidden}
  .scen-head{padding:18px 22px;color:#fff;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:10px}
  .scen-head.bull{background:var(--pos)}.scen-head.base{background:var(--ink)}.scen-head.bear{background:var(--crimson)}
  .scen-head h3{font-size:22px;letter-spacing:-.01em}
  .scen-head .tag{font-family:"SF Mono",ui-monospace,monospace;font-size:11px;letter-spacing:.12em;text-transform:uppercase;opacity:.85}
  .scen-body{padding:22px 22px 24px;background:var(--paper)}
  .scen-body .narr{font-size:16px;max-width:70ch;margin-bottom:20px}
  .drivers{display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
  .drivers .d{border:1px solid var(--line);border-radius:5px;padding:12px;background:var(--paper-2)}
  .drivers .d span{font-family:"SF Mono",ui-monospace,monospace;font-size:9px;letter-spacing:.1em;
    text-transform:uppercase;color:var(--mut);display:block;margin-bottom:5px}
  .drivers .d b{font-size:15px;font-family:"SF Mono",ui-monospace,monospace;display:block}
  .drivers .d .x{font-size:12px;color:var(--ink-2);display:block;margin-top:3px;line-height:1.35}
  .scen-out{margin-top:18px;border-top:1px solid var(--line);padding-top:16px;display:flex;
    justify-content:space-between;align-items:baseline;flex-wrap:wrap;gap:10px}
  .scen-out .label{font-family:"SF Mono",ui-monospace,monospace;font-size:10px;letter-spacing:.12em;text-transform:uppercase;color:var(--mut)}
  .scen-out .val{font-size:30px;font-family:"SF Mono",ui-monospace,monospace;font-weight:600}
  .scen-out.bull .val{color:var(--pos)}.scen-out.base .val{color:var(--ink)}.scen-out.bear .val{color:var(--crimson)}
  @media(max-width:680px){.drivers{grid-template-columns:1fr 1fr}}

  .risks{display:grid;grid-template-columns:repeat(2,1fr);gap:14px;margin-top:22px}
  .risk{border:1px solid var(--crimson);border-radius:5px;padding:16px;background:rgba(155,45,45,.04)}
  .risk h5{font-size:16px;margin-bottom:6px;color:var(--crimson)}
  .risk p{font-size:14px;color:var(--ink-2);margin:0}
  .risk .reb{display:block;margin-top:8px;font-size:13px;color:var(--teal-d);border-top:1px dashed var(--line);padding-top:7px}
  .risk .reb b{font-family:"SF Mono",ui-monospace,monospace;font-size:9px;letter-spacing:.1em;text-transform:uppercase;display:block;margin-bottom:2px}
  @media(max-width:620px){.risks{grid-template-columns:1fr}}

  .verdict{border:2px solid var(--ink);border-radius:6px;padding:24px;margin-top:28px;background:var(--paper-2)}
  .verdict .eyebrow{color:var(--amber)}
  .verdict p{font-size:16px;max-width:72ch}.verdict p+p{margin-top:12px}

  footer{padding:34px 0 56px;font-size:12px;color:var(--mut);border-top:1px solid var(--line);margin-top:10px}
  footer .disc{max-width:84ch;line-height:1.55}
</style>
</head>
<body>

<div class="mast">
  <div class="wrap">
    <div class="top">
      <div>
        <div class="kick">The decide layer · one position</div>
        <h1 class="title">The case for <em>Tenable.</em></h1>
      </div>
      <div class="author"><b>Arnav Bagchi Chowdhury</b>Independent equity research<br>Quality-at-a-discount · macro overlay</div>
    </div>
  </div>
</div>

<nav class="tabs">
  <div class="wrap">
    <button data-tab="tenable" class="headline active"><span class="n">★</span> The Case for Tenable</button>
    <button data-tab="industry"><span class="n">01</span> The Setup</button>
    <button data-tab="players"><span class="n">02</span> The Field</button>
    <button data-tab="mythos"><span class="n">03</span> The Catalyst</button>
    <button data-tab="scenarios"><span class="n">04</span> Scenarios</button>
    <button data-tab="risks"><span class="n">05</span> Risks &amp; Verdict</button>
  </div>
</nav>

<!-- ★ TENABLE — CENTERPIECE -->
<div class="panel show" id="tenable">
  <section><div class="wrap">
    <div class="tn-hero">
      <div class="eyebrow"><span class="num">★</span> The position</div>
      <h2>The cheapest, purest, best-validated way to own <em>the layer AI promotes.</em></h2>
      <p class="lead">As AI commoditises vulnerability <em>discovery</em>, value migrates to the layer that turns a flood of findings into prioritised, automated action — exposure management. Tenable is the leading listed pure-play on that layer, trading at a price that asks almost nothing of the future.</p>
      <div class="tn-stats">
        <div class="s"><span>Fwd P/E</span><b>~12×</b><span class="x">near its cheapest ever, vs 50–90× for the consolidators</span></div>
        <div class="s"><span>Recurring rev</span><b>~95%</b><span class="x">~$1bn revenue, ~82% gross margin</span></div>
        <div class="s"><span>Platform mix</span><b>~⅓</b><span class="x">Tenable One, growing mid-teens, targeted &gt;50% by FY29</span></div>
        <div class="s"><span>Validation</span><b>Glasswing</b><span class="x">direct Anthropic / Claude partnership in Hexa AI</span></div>
      </div>
    </div>

    <h3 class="sub">Three pillars of the bull case</h3>
    <div class="pillars">
      <div class="pillar"><div class="ph"><span class="pn">01</span> Quality franchise</div>
        <div class="pc"><h4>The category leader, and it's real</h4>
        <p>VM leader anchored by Nessus — the deepest, most accurate commercial scanning heritage in the industry. ~95% recurring revenue, ~82% gross margins, ~44,000 customers, 1.7T security findings across 300k+ sensor plugins. This is a high-quality, sticky, cash-generative software business, not a turnaround.</p></div></div>
      <div class="pillar"><div class="ph"><span class="pn">02</span> Mispriced overhang</div>
        <div class="pc"><h4>Cheap for a fixable reason</h4>
        <p>An "AI kills the scanner" fear has compressed the multiple to ~12× forward earnings / single-digit EV/FCF — near the cheapest in its history — even as the franchise stays intact and AI arguably <em>raises</em> demand for what it sells. That's an identifiable, resolvable reason for the discount: exactly the setup the framework looks for.</p></div></div>
      <div class="pillar"><div class="ph"><span class="pn">03</span> Structural tailwind</div>
        <div class="pc"><h4>The pivot is in the numbers</h4>
        <p>Tenable One is already ~⅓ of revenue, growing mid-teens, with a credible path to &gt;50% by FY29 — the mix-shift that drives the Rule-of-40 target. Unlike peers whose pivot is mostly narrative, Tenable's is <em>visible in the reported mix today.</em></p></div></div>
    </div>

    <h3 class="sub">Why it can defend itself — the moat boundary, honestly drawn</h3>
    <p class="body">The fair objection is that consolidators (CrowdStrike from the endpoint, Wiz/Microsoft from the cloud) are pushing into the same decide layer. Tenable's moat is real but bounded — here's exactly where it holds and where it doesn't.</p>
    <div class="moat">
      <div class="mh"><div class="a">Where Tenable holds</div><div class="b">Where it's contested</div></div>
      <div class="mb">
        <div class="a"><ul>
          <li><strong>Breadth across the awkward estate</strong> — OT / industrial control, Active Directory, hybrid & on-prem, the long tail of unmanaged assets endpoint agents can't see.</li>
          <li><strong>Source-agnostic neutrality</strong> — ingests anyone's findings (Open Connector, 300+ integrations); the "Switzerland" that multi-vendor enterprises prefer.</li>
          <li><strong>Detection-data edge</strong> — surfaces active exploitation ~7 days ahead of CISA's KEV catalog, with materially greater coverage.</li>
        </ul></div>
        <div class="b"><ul>
          <li><strong>Cloud-native ground</strong> — Wiz (now Microsoft) is the gold standard here and is building source-agnostic ingestion to attack the neutrality moat directly.</li>
          <li><strong>The intelligence layer</strong> — CrowdStrike already owns the agent + telemetry flywheel and can bundle exposure management near-free.</li>
          <li><strong>The aggregator middle</strong> — Brinqa, Vulcan, Nucleus prove the decide layer can be unbundled from the scanner entirely.</li>
        </ul></div>
      </div>
    </div>
    <p class="annot">The case is not "Tenable wins exposure management." It's "Tenable owns a defensible, hard-to-replicate corner of it — breadth + OT + neutrality — and you're paying ~12× for it while the contesters trade at 50–90×."</p>

    <h3 class="sub">The product that proves they understand the shift — Hexa AI</h3>
    <p class="body">Hexa AI, GA at the May Investor Day, is Tenable's agentic remediation engine — a Claude-powered (model-agnostic) harness on top of the Exposure Data Fabric that moves the platform from "system of record" to "system of action": ingest findings, prioritise by business risk, auto-create tickets, orchestrate the fix. Strategically it's the right product, and it's the clearest evidence management knows where value is going. The honest caveat, kept in view: today the bundled tokens cover only a few weeks of heavy use and the Foundation tier is a ~6% uplift — built to drive <em>adoption</em>, not yet to move <em>revenue</em>. The signal to watch is metered Hexa consumption showing up as a real line.</p>

    <div class="crit">
      <div><h6>Framework fit · gate 1</h6><p>Quality franchise — durable VM leadership, high returns on capital, ~95% recurring.</p></div>
      <div><h6>Framework fit · gate 2–3</h6><p>Resolvable overhang + multi-year secular tailwind (exposure management / CTEM), not a cyclical peak.</p></div>
      <div><h6>Framework fit · gate 4</h6><p>Passes the hard valuation gate comfortably — ~12× vs a cohort at 50–90×. This is the rare one that's actually cheap.</p></div>
    </div>
  </div></section>
</div>

<!-- 01 SETUP -->
<div class="panel" id="industry">
  <section><div class="wrap">
    <div class="shiftbox">
      <div class="shift-h">Why this matters — where the money sits, before &amp; after AI</div>
      <div class="shiftgrid">
        <div class="col before"><h4>Old loop · scarce = finding</h4>
          <div class="stack">
            <div class="layer det"><span class="lab">High value</span>Find the vulnerabilities — scan everything</div>
            <div class="layer val"><span class="lab">Lower value</span>Decide what to fix first</div>
            <div class="layer val"><span class="lab">Lower value</span>Actually fix it</div>
          </div></div>
        <div class="arrowcol"><div class="ar">&rarr;</div></div>
        <div class="col after"><h4>New loop · scarce = triage</h4>
          <div class="stack">
            <div class="layer det dim"><span class="lab">Commoditising</span>Find — AI now does this at scale</div>
            <div class="layer val hot"><span class="lab">Value migrates here</span>Decide what to fix, out of a flood</div>
            <div class="layer val hot"><span class="lab">Value migrates here</span>Orchestrate the fix at machine speed</div>
          </div></div>
      </div>
      <p class="shift-cap">When finding was hard, the scanner was the prize. When AI makes findings near-infinite, the prize becomes the layer that turns a flood into "fix these seven things, now" — <strong style="color:#7FC9C4;font-style:normal">exposure management.</strong> That is the layer Tenable is built on.</p>
    </div>
    <div class="eyebrow"><span class="num">1</span> The setup — how the industry works</div>
    <h2>"Cybersecurity" is a <em>stack of jobs,</em> not one business.</h2>
    <p class="lead">The companies people lump together rarely compete head-to-head — they live on different rungs. Tenable lives on the two rungs AI is reshaping: Find, and increasingly, Decide.</p>
    <div class="stackmap">
      <div class="row"><div class="tag"><b>Find</b><span>Exposure / VM</span></div>
        <div class="desc">Inventory every asset, flag weaknesses <em>before</em> attack. Per-asset subscription.<span class="who">Tenable · Qualys · Rapid7</span></div></div>
      <div class="row"><div class="tag"><b>Stop</b><span>Endpoint / EDR</span></div>
        <div class="desc">Sit on the device, stop attacks in real time. Data network effect compounds.<span class="who">CrowdStrike · SentinelOne · Microsoft</span></div></div>
      <div class="row"><div class="tag"><b>Gatekeep</b><span>Network / Access</span></div>
        <div class="desc">Control what gets in, who reaches what — firewalls, secure access, cloud.<span class="who">Palo Alto · Zscaler · Fortinet</span></div></div>
      <div class="row hl"><div class="tag"><b>Decide</b><span>Prioritise / Orchestrate</span></div>
        <div class="desc">Signals from <em>everywhere</em>, ranked by business risk, fix driven. <strong>The rung AI promotes — and Tenable's destination.</strong><span class="who">Tenable One · Wiz · Qualys ETM · CrowdStrike Fusion</span></div></div>
    </div>
  </div></section>
</div>

<!-- 02 FIELD -->
<div class="panel" id="players">
  <section><div class="wrap">
    <div class="eyebrow"><span class="num">2</span> The field — who Tenable is up against</div>
    <h2>The competitive set. <em>Tap each to open.</em></h2>
    <p class="lead">Two pure-play peers, two consolidators pressing in from above and beside. The threats are real — which is why Tenable's discount exists, and why the moat boundary matters.</p>
    <div class="players">
      <div class="pcard spot">
        <button class="phead"><span><h4>Tenable ★</h4><span class="tick">NASDAQ: TENB</span><span class="role">Find → Decide · the position</span></span><span class="chev">+</span></button>
        <div class="pbody"><div class="inner">
          <p>The subject of this piece. VM leader pivoting into exposure management via Tenable One; deepest non-cloud breadth (OT, AD, hybrid) and source-agnostic. Cheapest of the set, with the most visible pivot. See "The Case for Tenable" tab.</p>
          <div class="stat"><div><span>Growth</span><b>~10%</b></div><div><span>Op margin</span><b>~24%</b></div><div><span>Fwd P/E</span><b>~12×</b></div><div><span>Pivot</span><b>visible</b></div></div>
        </div></div>
      </div>
      <div class="pcard">
        <button class="phead"><span><h4>Qualys</h4><span class="tick">NASDAQ: QLYS</span><span class="role">Find → Decide · the cash machine</span></span><span class="chev">+</span></button>
        <div class="pbody"><div class="inner">
          <p>Same pivot, earlier (exposure mgmt ~11% of bookings). Higher quality on the numbers — ~47% EBITDA margins, net cash, buyback — but no frontier-lab partnership and a less-proven transition. The better business; the weaker vehicle for <em>this</em> thesis.</p>
          <div class="stat"><div><span>Growth</span><b>~10%</b></div><div><span>EBITDA mgn</span><b>~47%</b></div><div><span>Fwd P/E</span><b>~18×</b></div><div><span>Pivot</span><b>early</b></div></div>
        </div></div>
      </div>
      <div class="pcard">
        <button class="phead"><span><h4>CrowdStrike</h4><span class="tick">NASDAQ: CRWD</span><span class="role">Stop → Decide · consolidator (endpoint)</span></span><span class="chev">+</span></button>
        <div class="pbody"><div class="inner">
          <p>Endpoint king with a real data flywheel, now bundling Falcon Exposure Management near-free off the agent it already ships. The chief threat from above — but doesn't natively cover OT / industrial, and wants you single-vendor. Priced for perfection.</p>
          <div class="stat"><div><span>Growth</span><b>~22%</b></div><div><span>Fwd P/E</span><b>~90×</b></div><div class="neg"><span>Val. gate</span><b>fails</b></div><div><span>Moat</span><b>wide</b></div></div>
        </div></div>
      </div>
      <div class="pcard">
        <button class="phead"><span><h4>Wiz / Microsoft</h4><span class="tick">private → MSFT</span><span class="role">Cloud → Decide · consolidator (cloud)</span></span><span class="chev">+</span></button>
        <div class="pbody"><div class="inner">
          <p>The gold standard in cloud exposure management, now inside Microsoft. Building source-agnostic ingestion (UVM/Dazz) to contest Tenable's neutrality, and Microsoft is folding Defender VM into an Exposure Management home. The chief threat from beside — strongest in cloud, weakest in OT/hybrid breadth.</p>
          <div class="stat"><div><span>Position</span><b>cloud</b></div><div><span>Owner</span><b>MSFT</b></div><div><span>Threat</span><b>high</b></div><div><span>Gap</span><b>OT/hybrid</b></div></div>
        </div></div>
      </div>
    </div>
    <p class="annot">Also in the frame: Rapid7 (third VM pure-play, cheaper/more troubled), SentinelOne (smaller EDR), and aggregator pure-plays Brinqa / Vulcan / Nucleus (mostly private). Figures approximate, FY25–FY26 reference.</p>
  </div></section>
</div>

<!-- 03 CATALYST -->
<div class="panel" id="mythos">
  <section><div class="wrap">
    <div class="feature">
      <div class="eyebrow" style="color:#E8B98C"><span class="num" style="color:#7FC9C4;border-color:#7FC9C4">3</span> The catalyst — Mythos &amp; Glasswing</div>
      <h2 style="color:var(--paper)">The moment finding stopped being <em style="color:#7FC9C4">the hard part.</em></h2>
      <p>Anthropic's most advanced model class showed AI can discover and chain software vulnerabilities at a scale no human team or legacy scanner matches. Through Project Glasswing, these capabilities surfaced more than 10,000 high- or critical-severity vulnerabilities in real, critical systems.</p>
      <p class="pull">For two decades, progress was limited by how fast you could <em>find</em> vulnerabilities. Now it's limited by how fast you can verify, prioritise and patch the flood AI uncovers.</p>
      <p>This is the catalyst for the Tenable thesis specifically. If detection is abundant, value drains out of "find" and pools in "decide" — and Tenable, via Tenable One and Hexa, is built on "decide." Crucially, Anthropic has said it wants to be a general AI platform, <em>not</em> a cyber vendor — so the labs amplify demand for Tenable's layer rather than competing with it. And Tenable is in the expanded Glasswing program with a direct Anthropic partnership, validation Qualys lacks.</p>
      <div class="gw">
        <div><h5>What Mythos does for Tenable</h5><p>Turns discovery into a firehose, multiplying the volume of findings Tenable's prioritisation and Hexa remediation layer exists to triage. More flood = more need for the decide layer.</p></div>
        <div><h5>What Glasswing signals</h5><p>The labs distribute capability <em>through</em> vendors. Tenable is a partner, not a target — and the named partner, not a bystander. Thesis-consistent validation from the source of the disruption itself.</p></div>
      </div>
    </div>
  </div></section>
</div>

<!-- 04 SCENARIOS -->
<div class="panel" id="scenarios">
  <section><div class="wrap">
    <div class="eyebrow"><span class="num">4</span> Scenarios — toggle the outcome</div>
    <h2>Does the AI wave drown Tenable, or <em>supercharge</em> it?</h2>
    <p class="lead">The bull case is the chain where the flood becomes the product. Click through all three — the case is only honest if the bear sits next to the bull.</p>
    <div class="scen-controls">
      <button data-s="bull"><span class="cl">Bull</span><span class="cv">2–3×</span><span class="cd">flood becomes the product</span></button>
      <button data-s="base" class="active"><span class="cl">Base</span><span class="cv">+30–50%</span><span class="cd">slow profitable grind</span></button>
      <button data-s="bear"><span class="cl">Bear</span><span class="cv">−20%</span><span class="cd">consolidator annexes it</span></button>
    </div>
    <div class="scen-panel" id="scenPanel"></div>
    <p class="annot">Illustrative ranges to frame a distribution, not price targets. No analyst consensus targets used.</p>
  </div></section>
</div>

<!-- 05 RISKS -->
<div class="panel" id="risks">
  <section><div class="wrap">
    <div class="eyebrow" style="color:var(--crimson)"><span class="num" style="color:var(--crimson);border-color:var(--crimson)">5</span> The honest risks — and the rebuttal</div>
    <h2>Why this could be wrong, and why I'd still take the bet.</h2>
    <p class="lead">The case is strong but not free. Each risk gets a fair statement and the strongest counter — the bet only holds if it survives its own bear case.</p>
    <div class="risks">
      <div class="risk"><h5>The consolidator owns the prize</h5><p>CrowdStrike (endpoint) and Wiz/Microsoft (cloud) are both pressing into the decide layer; they own telemetry and bundle for near-free.</p>
        <span class="reb"><b>The rebuttal</b>Neither natively covers OT / industrial / hybrid breadth, and both want single-vendor lock-in. Tenable's neutrality + breadth is a real, if narrow, corner — and you're paid for the risk at ~12×, not 90×.</span></div>
      <div class="risk"><h5>Reacceleration is a model, not a fact</h5><p>The FY29 Rule-of-40 target leans on Tenable One dragging total growth up; today growth is ~10% and decelerating. Careful analysts left it out of their numbers.</p>
        <span class="reb"><b>The rebuttal</b>You're not paying for the reacceleration — at ~12× it's free optionality. The mix-shift is already visible in reported segments, not just promised.</span></div>
      <div class="risk"><h5>AI revenue is thin today</h5><p>Hexa's bundled tokens cover a few weeks of use; Foundation is a ~6% uplift — adoption tool, not yet revenue.</p>
        <span class="reb"><b>The rebuttal</b>Correct, and that's the point: none of the AI upside is in the price. Metered consumption converting later is upside, not the thesis.</span></div>
      <div class="risk"><h5>"Wrong attacker" defence</h5><p>Tenable dismissed the labs (no sensors) — but two-thirds of breaches are identity/misconfig, which is CrowdStrike's turf, not the labs'.</p>
        <span class="reb"><b>The rebuttal</b>Identity & misconfig across hybrid/OT is exactly where Tenable's breadth (AD, Ermetic CIEM) is strongest — it's contested, not conceded.</span></div>
      <div class="risk"><h5>Dead money / opportunity cost</h5><p>A cheap stock can stay cheap. The real risk may be two flat years awaiting an inflection.</p>
        <span class="reb"><b>The rebuttal</b>Even the bear is ~−20%, not a blow-up — and you compound ~10% cash-generative earnings while waiting. Asymmetric, not binary.</span></div>
      <div class="risk"><h5>Concentration &amp; macro</h5><p>~15% government revenue (budget cycles), channel/distributor concentration, carried debt, high-multiple-cohort sensitivity.</p>
        <span class="reb"><b>The rebuttal</b>Government exposure is mission-critical/sticky; the low multiple is itself the cushion against a software-cohort de-rating.</span></div>
    </div>

    <div class="verdict">
      <div class="eyebrow">The verdict</div>
      <p><strong>Tenable is the cheapest, purest, best-validated listed way to own the layer AI promotes — a defensible specialist at ~12× with a visible pivot and a frontier-lab partnership.</strong></p>
      <p>It is not the widest moat in cybersecurity; that belongs to consolidators priced for perfection. The position is a deliberate wager that a <em>narrow</em> moat at a <em>fair</em> price, in front of a genuine structural tailwind, beats paying 50–90× for a wide one — with the AI upside sitting as free optionality on top of a quality, cash-generative franchise. Eyes open to the chance the consolidators annex the rung; paid, at ~12×, to take that chance.</p>
    </div>
  </div></section>

  <footer><div class="wrap"><p class="disc"><strong>For independent research and discussion only.</strong> Not investment advice, not a recommendation, not a solicitation to buy or sell any security. The author is not a registered investment adviser. Figures are approximate, drawn from company reporting (FY25–FY26) and prevailing market multiples, used for reference and stress-testing rather than precise valuation; multiples and prices change. Scenario outcomes are illustrative ranges framing a distribution of possibilities, not price targets; no analyst consensus targets are used. Forward-looking statements are inherently uncertain. Do your own work and consult a licensed professional before any investment decision. · Arnav Bagchi Chowdhury</p></div></footer>
</div>

<script>
  const tabs=document.querySelectorAll('nav.tabs button');
  const panels=document.querySelectorAll('.panel');
  tabs.forEach(b=>b.addEventListener('click',()=>{
    tabs.forEach(x=>x.classList.remove('active'));
    panels.forEach(p=>p.classList.remove('show'));
    b.classList.add('active');
    document.getElementById(b.dataset.tab).classList.add('show');
    window.scrollTo({top:0,behavior:'instant'});
  }));
  document.querySelectorAll('.pcard .phead').forEach(btn=>{
    btn.addEventListener('click',()=>btn.closest('.pcard').classList.toggle('open'));
  });
  const scenData={
    bull:{tag:'Findings overwhelm the team → triage becomes the product',title:'The flood becomes the product',cls:'bull',
      narr:'AI-driven discovery — plus an AI-expanded attack surface of more agents, identities and apps — pushes findings past what any team can triage by hand. The pain turns acute and universal. Buyers stop shopping for scanners and pay up for one pane of glass that decides what to fix. Tenable One conversions accelerate; Hexa\u2019s machine-speed remediation turns "system of record" into "system of action" and gets metered as usage. Platform mix crosses 50% ahead of plan, total growth re-accelerates into the teens, NRR expands — and the market re-rates a re-accelerating compounder from ~12× toward 20×+.',
      d:[['Tenable One mix','>50%','ahead of FY29 plan'],['Total growth','mid-teens','reaccelerates'],['Hexa revenue','metered','usage scales'],['Multiple','~20×+','re-rate']],
      out:'2–3×',outlbl:'multiple re-rate × growth, multi-year'},
    base:{tag:'Mix-shift works, but gradually',title:'A slow, profitable grind up',cls:'base',
      narr:'The mix-shift works but gradually. Tenable One keeps compounding mid-teens, standalone VM holds mid-single-digits, total growth stays ~7–10%, margins expand ~125–150bps a year toward the Rule-of-40 target by FY29. No dramatic re-rating — but a cheap, cash-generative business compounding earnings. You\u2019re paid to wait while the thesis proves out in the prints.',
      d:[['Tenable One mix','rising','to FY29'],['Total growth','~7–10%','steady'],['Margins','+125–150bps/yr','Rule of 40 by FY29'],['Multiple','~12–15×','little change']],
      out:'+30–50%',outlbl:'earnings growth + modest re-rate'},
    bear:{tag:'A consolidator captures the decide layer',title:'The consolidator annexes the rung',cls:'bear',
      narr:'The decide layer is real — but a consolidator captures it. CrowdStrike bundles exposure management near-free off its agent, or Wiz/Microsoft wins it inside the Microsoft estate. CISOs stop buying a separate Tenable contract. The mix-shift stalls, growth stays stuck in single digits, and "cheap" turns out to be the market correctly pricing a niche specialist whose ceiling is capped from above.',
      d:[['Tenable One mix','stalls','migration slows'],['Total growth','low single','stuck'],['Win rate','slips','vs CRWD / Wiz'],['Multiple','~10×','de-rate / trap']],
      out:'−20%',outlbl:'value trap, upside capped from above'}
  };
  const panel=document.getElementById('scenPanel');
  function renderScen(k){
    const s=scenData[k];
    panel.innerHTML=
      '<div class="scen-head '+s.cls+'"><h3>'+s.title+'</h3><span class="tag">'+s.tag+'</span></div>'+
      '<div class="scen-body"><p class="narr">'+s.narr+'</p>'+
      '<div class="drivers">'+s.d.map(x=>'<div class="d"><span>'+x[0]+'</span><b>'+x[1]+'</b><span class="x">'+x[2]+'</span></div>').join('')+'</div>'+
      '<div class="scen-out '+s.cls+'"><span class="label">Illustrative outcome</span><span class="val">'+s.out+'</span></div>'+
      '<p class="annot" style="margin-top:6px">'+s.outlbl+'</p></div>';
  }
  document.querySelectorAll('.scen-controls button').forEach(b=>{
    b.addEventListener('click',()=>{
      document.querySelectorAll('.scen-controls button').forEach(x=>x.classList.remove('active'));
      b.classList.add('active');renderScen(b.dataset.s);
    });
  });
  renderScen('base');
</script>
</body>
</html>
