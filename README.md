# U.S.-Government-Investments-in-Rare-Earths-and-Permanent-Magnets-1[us_rare_earths_investment_bubble_chart.html](https://github.com/user-attachments/files/28358110/us_rare_earths_investment_bubble_chart.html)

<h2 class="sr-only">Bubble chart of U.S. Government Investments in Rare Earths and Permanent Magnets. Each bubble represents a project, sized by investment in USD millions, colored by agency (EXIM, DOD, Commerce, DFC, USTDA) across eight countries.</h2>

<div style="padding: 1rem 0.5rem 1.5rem; background: #fff;">
  <p style="font-size: 13px; font-weight: 500; color: #1a1a1a; margin: 0 0 3px; line-height: 1.4;">U.S. Government Investments in Rare Earths and Permanent Magnets</p>
  <p style="font-size: 11.5px; color: #666; margin: 0 0 14px;">Each bubble represents a project, sized by investment amount in USD millions, colored by agency.</p>

  <div style="display: flex; flex-wrap: wrap; gap: 6px 18px; margin-bottom: 14px;">
    <span style="display:flex;align-items:center;gap:5px;font-size:12px;color:#333;"><span style="width:11px;height:11px;border-radius:50%;background:#4E9FD1;display:inline-block;"></span>EXIM</span>
    <span style="display:flex;align-items:center;gap:5px;font-size:12px;color:#333;"><span style="width:11px;height:11px;border-radius:50%;background:#2D9D6E;display:inline-block;"></span>DOD</span>
    <span style="display:flex;align-items:center;gap:5px;font-size:12px;color:#333;"><span style="width:11px;height:11px;border-radius:50%;background:#C45A30;display:inline-block;"></span>Commerce</span>
    <span style="display:flex;align-items:center;gap:5px;font-size:12px;color:#333;"><span style="width:11px;height:11px;border-radius:50%;background:#B8893A;display:inline-block;"></span>DFC</span>
    <span style="display:flex;align-items:center;gap:5px;font-size:12px;color:#333;"><span style="width:11px;height:11px;border-radius:50%;background:#C06080;display:inline-block;"></span>USTDA</span>
  </div>

  <div style="position:relative;width:100%;height:480px;">
    <canvas id="bc" role="img" aria-label="Bubble chart showing U.S. government investments across Australia, United States, Canada, Greenland, Brazil, Angola, Mozambique, Saudi Arabia by agency.">Largest investment: Commerce ~$1.6B in United States. Significant EXIM investments in Australia and United States (~$600M each). DFC ~$580M in Brazil.</canvas>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
const ctries = ['Australia','United States','Canada','Greenland','Brazil','Angola','Mozambique','Saudi Arabia'];
function r(v){ return Math.sqrt(v)*0.93; }

const ds = [
  {
    label:'EXIM',
    backgroundColor:'rgba(78,159,209,0.68)',
    borderColor:'rgba(55,130,180,0.9)',
    borderWidth:1,
    data:[
      {x:-0.15,y:600,r:r(600)},{x:0.12,y:572,r:r(572)},
      {x:-0.05,y:292,r:r(292)},{x:0.22,y:202,r:r(202)},
      {x:-0.22,y:172,r:r(172)},{x:0.06,y:88,r:r(88)},
      {x:0.82,y:600,r:r(600)},{x:1.08,y:558,r:r(558)},
      {x:1.28,y:532,r:r(532)},{x:1.0,y:202,r:r(202)},
      {x:1.18,y:148,r:r(148)},{x:0.88,y:47,r:r(47)},
      {x:1.27,y:36,r:r(36)},
      {x:2.0,y:212,r:r(212)},
      {x:3.0,y:122,r:r(122)},
      {x:5.0,y:162,r:r(162)}
    ]
  },
  {
    label:'DOD',
    backgroundColor:'rgba(45,157,110,0.68)',
    borderColor:'rgba(25,130,85,0.9)',
    borderWidth:1,
    data:[
      {x:0.73,y:648,r:r(648)},{x:0.93,y:612,r:r(612)},
      {x:0.83,y:96,r:r(96)},{x:0.98,y:66,r:r(66)},
      {x:7.0,y:80,r:r(80)}
    ]
  },
  {
    label:'Commerce',
    backgroundColor:'rgba(196,90,48,0.68)',
    borderColor:'rgba(175,70,30,0.9)',
    borderWidth:1,
    data:[{x:1.2,y:1600,r:r(1600)}]
  },
  {
    label:'DFC',
    backgroundColor:'rgba(184,137,58,0.68)',
    borderColor:'rgba(160,115,35,0.9)',
    borderWidth:1,
    data:[{x:4.0,y:578,r:r(578)}]
  },
  {
    label:'USTDA',
    backgroundColor:'rgba(192,96,128,0.68)',
    borderColor:'rgba(168,75,105,0.9)',
    borderWidth:1,
    data:[{x:6.0,y:26,r:r(26)}]
  }
];

new Chart(document.getElementById('bc'),{
  type:'bubble',
  data:{datasets:ds},
  options:{
    responsive:true,
    maintainAspectRatio:false,
    layout:{padding:{top:44,right:16,bottom:4,left:4}},
    plugins:{
      legend:{display:false},
      tooltip:{
        backgroundColor:'rgba(255,255,255,0.96)',
        borderColor:'rgba(0,0,0,0.12)',
        borderWidth:1,
        titleColor:'#1a1a1a',
        bodyColor:'#444',
        callbacks:{
          title:()=>'',
          label:(ctx)=>{
            const v=ctx.raw.y;
            const ci=Math.round(ctx.raw.x);
            const country=ctries[Math.max(0,Math.min(7,ci))];
            const agency=ctx.dataset.label;
            const fmt=v>=1000?'$'+(v/1000).toFixed(1)+'B':'$'+v+'M';
            return ` ${agency} · ${country}: ${fmt}`;
          }
        }
      }
    },
    scales:{
      x:{
        min:-0.55,
        max:7.55,
        grid:{color:'rgba(0,0,0,0.06)',lineWidth:1},
        border:{display:false},
        afterBuildTicks:(ax)=>{ax.ticks=[0,1,2,3,4,5,6,7].map(v=>({value:v}));},
        ticks:{
          font:{size:12},
          color:'#555',
          maxRotation:0,
          minRotation:0,
          callback:(v)=>Number.isInteger(v)?(ctries[v]??''):''
        }
      },
      y:{
        min:0,
        max:1900,
        grid:{color:'rgba(0,0,0,0.06)',lineWidth:1},
        border:{display:false},
        title:{
          display:true,
          text:'Investment (USD)',
          font:{size:11.5},
          color:'#666'
        },
        ticks:{
          font:{size:11},
          color:'#555',
          stepSize:200,
          callback:(v)=>{
            if(v===0)return '$0';
            if(v>=1000)return '$'+(v/1000).toFixed(1)+'B';
            return '$'+v+'M';
          }
        }
      }
    }
  }
});
</script>
