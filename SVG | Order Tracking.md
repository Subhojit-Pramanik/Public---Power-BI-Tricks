SVG | Order tracking = 

VAR _OrderDate = FORMAT( SELECTEDVALUE(Orders[Order Date]), "d mmm yy")
VAR _PackedDate = FORMAT( SELECTEDVALUE(Orders[Packed Date]), "d mmm yy")
VAR _ShippedDate = FORMAT( SELECTEDVALUE(Orders[Shipped Date]), "d mmm yy")
VAR _DeliveredDate = FORMAT( SELECTEDVALUE(Orders[Received Date]), "d mmm yy")
VAR _Transit = [In Transit Days]
VAR _TransitDays = IF(NOT(ISBLANK(_Transit)), _Transit & " days")
VAR _OrderStatus = [Order Status V2]


VAR _txtColor = "#9AA6B2"
VAR _IncompleteColor = "#BCCCDC"
VAR _CompleteColor = "#2C9CD0"

VAR _PackedColor = IF(_PackedDate = "", _IncompleteColor, _CompleteColor)
VAR _ShippedColor = IF(_ShippedDate = "", _IncompleteColor, _CompleteColor)
VAR _DeliveredColor = IF(_DeliveredDate = "", _IncompleteColor, _CompleteColor)
VAR _TransitColor = IF(ISBLANK(_Transit), _IncompleteColor, _CompleteColor)
VAR _StatusColor = 
SWITCH(
    TRUE(),
    CONTAINSSTRING(_OrderStatus, "Early"), "Green",
    CONTAINSSTRING(_OrderStatus, "Late"), "Red",
    _CompleteColor
)


VAR _OrderPlacedIcon = 
"<path fill='"&_CompleteColor&"' fill-rule='evenodd' d='M25 12.5a6.25 6.25 0 0 1 6.25-6.25h37.5A6.25 6.25 0 0 1 75 12.5V25h.688a6.25 6.25 0 0 1 6.062 4.731l1.563 6.25a6.249 6.249 0 0 1-6.063 7.769H75v3.125h3.125a6.25 6.25 0 0 1 6.25 6.25v3.125a6.25 6.25 0 0 1-6.25 6.25H75V75a6.25 6.25 0 0 1-6.25 6.25H54.419l-1.85 1.85-5.163 10.319a6.25 6.25 0 0 1-5.587 3.456h-19a6.25 6.25 0 0 1-3.463-1.05l-7.2-4.8a6.25 6.25 0 0 1-2.781-5.2v-23.1c0-.297.02-.593.063-.888l5.837-40.843a6.25 6.25 0 0 1 6.187-5.369H25V12.5Zm0 9.375h-3.538l-5.837 40.85v23.1l7.194 4.8h5.306v-8.331a6.25 6.25 0 0 1 1.25-3.75l16.5-22-5.25-5.25-13.413 13.419-4.424-4.425L25 58.08V21.875Zm6.25 29.956 4.956-4.956a6.25 6.25 0 0 1 8.838 0l5.25 5.25a6.25 6.25 0 0 1 .581 8.169L39.844 75H68.75V12.5h-37.5v39.331ZM75 37.5h2.25l-1.563-6.25H75v6.25Zm0 15.625v3.125h3.125v-3.125H75ZM35.156 81.25l-.781 1.044v8.331h7.444l4.687-9.375h-11.35Zm11.719-59.375V18.75h6.25v3.125h-6.25Zm3.125 0a9.375 9.375 0 0 0-9.375 9.375H37.5v6.25h25v-6.25h-3.125A9.375 9.375 0 0 0 50 21.875Zm0 6.25a3.125 3.125 0 0 0-3.125 3.125h6.25A3.125 3.125 0 0 0 50 28.125ZM38.413 61.587l-3.125-3.125 4.425-4.425 3.124 3.126-4.425 4.425Z' clip-rule='evenodd'/>"

VAR _PackedIcon = 
"
    <path d='M88.25 25L53.875 5.3125C52.689 4.65587 51.3556 4.31138 50 4.31138C48.6444 4.31138 47.311 4.65587 46.125 5.3125L11.75 25C10.5497 25.6856 9.55272 26.6775 8.86097 27.8743C8.16922 29.0712 7.80742 30.4301 7.8125 31.8125V68.75C7.90234 70.0357 8.30889 71.2793 8.99591 72.3698C9.68292 73.4603 10.6291 74.3639 11.75 75L46.125 94.4375C47.311 95.0941 48.6444 95.4386 50 95.4386C51.3556 95.4386 52.689 95.0941 53.875 94.4375L88.25 75C89.3709 74.3639 90.3171 73.4603 91.0041 72.3698C91.6911 71.2793 92.0977 70.0357 92.1875 68.75V31.5625C92.1492 30.2228 91.7669 28.9154 91.0774 27.7661C90.3878 26.6168 89.4141 25.6642 88.25 25ZM46.125 85.6875L32.8125 78.1875V45.0625L46.125 52.3125V85.6875ZM50 45.5625L37 38.4375L67.0625 21.75L80.125 29.125L50 45.5625ZM50 12.125L59.125 17.25L28.875 34.0625L19.875 29.125L50 12.125ZM15.625 35.6875L25 40.8125V73.75L15.625 68.75V35.6875ZM53.875 85.6875V52.3125L84.375 35.6875V68.75L53.875 85.6875Z' fill='"&_PackedColor&"'/>
  "

VAR _ShippedIcon = 
"
<path fill='"&_ShippedColor&"' d='M89.583 75H60.417V29.167H82.5c1.875 0 3.333 1.25 3.958 2.916l7.292 22.084v16.666A4.179 4.179 0 0 1 89.583 75Zm-29.166 0h-50a4.179 4.179 0 0 1-4.167-4.167V18.75a4.179 4.179 0 0 1 4.167-4.167H56.25a4.179 4.179 0 0 1 4.167 4.167V75Z'/>
  <path fill='#37474F' d='M77.083 85.417C82.836 85.417 87.5 80.753 87.5 75s-4.664-10.417-10.417-10.417S66.667 69.247 66.667 75s4.663 10.417 10.416 10.417Zm-50 0C32.836 85.417 37.5 80.753 37.5 75s-4.664-10.417-10.417-10.417S16.667 69.247 16.667 75s4.663 10.417 10.416 10.417Z'/>
  <path fill='#78909C' d='M77.083 79.167a4.167 4.167 0 1 0 0-8.334 4.167 4.167 0 0 0 0 8.334Zm-50 0a4.167 4.167 0 1 0 0-8.334 4.167 4.167 0 0 0 0 8.334Z'/>
  <path fill='#37474F' d='M85.417 52.083H70.833c-1.25 0-2.083-.833-2.083-2.083V35.417c0-1.25.833-2.084 2.083-2.084h11.042c.833 0 1.667.625 1.875 1.459l3.542 10.833c0 .208.208.417.208.625V50c0 1.25-.833 2.083-2.083 2.083Z'/>
  <path fill='#fff' d='M45.417 28.75 28.958 45.208l-7.708-7.916-4.583 4.583 12.291 12.292L50 33.125l-4.583-4.375Z'/>
 "

VAR _InTransitIcon = 
"<path fill='"&_TransitColor&"' d='M0 15.385v3.846h30.77v3.846H7.691v3.846H0v3.846h26.923v3.846H7.693v3.846H0v3.847h23.077v3.846H7.692V50H0v3.846h19.23v3.846H7.693v15.385c0 2.308 1.539 3.846 3.847 3.846h3.846c.769-6.538 6.538-11.9 13.461-11.9S41.538 70 42.308 76.923h11.538c2.308 0 3.846-1.538 3.846-3.846V19.23c0-2.308-1.538-3.846-3.846-3.846H0Zm65.385 15.384c-2.308 0-3.847 1.539-3.847 3.846v38.462c0 1.923 1.539 3.846 3.847 3.846.769-6.538 6.538-11.9 13.461-11.9S91.538 70 92.308 76.923h3.846c2.308 0 3.846-1.538 3.846-3.846v-19.23c0-3.462-3.127-7.693-3.127-7.693l-8.412-11.539c-1.922-2.307-3.076-3.846-5.769-3.846H65.385Zm7.692 7.693h9.254c.769 0 1.565.723 1.565.723l8.05 11.176c.77 1.154 1.566 2.354 1.566 3.124H73.076V38.462Zm-44.23 31.492a8.924 8.924 0 0 0-8.897 8.892 8.923 8.923 0 0 0 8.896 8.896 8.923 8.923 0 0 0 8.896-8.896 8.919 8.919 0 0 0-8.896-8.892Zm50 0a8.924 8.924 0 0 0-8.897 8.892 8.923 8.923 0 0 0 8.896 8.896 8.923 8.923 0 0 0 8.896-8.896 8.919 8.919 0 0 0-8.896-8.892Z'/>"

VAR _DeliveredIcon = 
"
<path fill='"&_DeliveredColor&"' d='M50 8.333c-.833 0-1.667.417-2.5.834L14.583 27.5c-1.25.833-2.083 2.083-2.083 3.75v37.5c0 1.667.833 2.917 2.083 3.75L47.5 90.833c.833.417 1.667.834 2.5.834s1.667-.417 2.5-.834l3.75-2.083c-1.25-2.5-1.667-5.417-2.083-8.333V52.5l25-14.167v15.834c2.916 0 5.833.416 8.333 1.25V31.25c0-1.667-.833-2.917-2.083-3.75L52.5 9.167c-.833-.417-1.667-.834-2.5-.834Zm0 9.167 25 13.75-8.333 4.583-24.584-14.166L50 17.5Zm-16.25 8.75 24.583 14.583L50 45.417 25 31.25l8.75-5ZM20.833 38.333l25 14.167v27.917l-25-14.167V38.333Zm67.917 27.5-15 15-6.667-6.666-4.583 5 11.667 12.5 20-20-5.417-5.834Z'/>
"

VAR _Svg = 

"
data:image/svg+xml;utf8,
<svg width='800' height='185' xmlns='http://www.w3.org/2000/svg'>
  <style>
    .circle { fill: #FFFFFF; stroke: _CompleteColor; }
    .text { font-family: Segoe UI; font-size: 20px; text-anchor: middle; dominant-baseline: middle; }
    .date { fill: "&_CompleteColor&"; font-family: Segoe UI; font-size: 16px; text-anchor: middle; dominant-baseline: middle; }
    .status { fill: "&_StatusColor&"; font-family: Segoe UI; font-size: 16px; text-anchor: middle; dominant-baseline: middle; }
    .line { stroke: #ccc; stroke-width: 4; }
  </style>

  <!-- Connecting line (ends before the last circle) -->
  <line x1='96' y1='60' x2='164' y2='60' stroke='"&_PackedColor&"' stroke-width='4' />
  <line x1='236' y1='60' x2='304' y2='60' stroke='"&_ShippedColor&"' stroke-width='4' />
  <line x1='376' y1='60' x2='444' y2='60' stroke='"&_TransitColor&"' stroke-width='4' />
  <line x1='516' y1='60' x2='588' y2='60' stroke='"&_DeliveredColor&"' stroke-width='4' />

  <!-- Step 1 -->
  <circle cx='60' cy='60' r='45' fill='#FFFFFF' stroke='"&_CompleteColor&"' />
  <g transform='translate(35, 30) scale(0.6)'>
  "&_OrderPlacedIcon&"
  </g>
  <text x='60' y='130' class='text' fill='"&_CompleteColor&"'>Order Placed</text>
  <text x='60' y='155' class='date'>"&_OrderDate&"</text>
  
  <!-- Step 2 -->
  <circle cx='210' cy='60' r='45' fill='#FFFFFF' stroke='"&_PackedColor&"' />
  <g transform='translate(180, 30) scale(0.6)'>
  "&_PackedIcon&"
  </g>
  <text x='210' y='130' class='text' fill='"&_PackedColor&"'>Packed</text>
  <text x='210' y='155' class='date'>"&_PackedDate&"</text>
  
  <!-- Step 3 -->
  <circle cx='350' cy='60' r='45' fill='#FFFFFF' stroke='"&_ShippedColor&"' />
  <g transform='translate(322, 30) scale(0.6)'>
  "&_ShippedIcon&"
  </g>
  <text x='350' y='130' class='text' fill='"&_ShippedColor&"'>Shipped</text>
  <text x='350' y='155' class='date'>"&_ShippedDate&"</text>

  <!-- Step 4 -->
  <circle cx='490' cy='60' r='45' fill='#FFFFFF' stroke='"&_TransitColor&"' />
  <g transform='translate(462, 30) scale(0.6)'>
  "&_InTransitIcon&"
  </g>
  <text x='490' y='130' class='text' fill='"&_TransitColor&"'>In Transit</text>
  <text x='490' y='155' class='date'>"&_TransitDays&"</text>
 
  <!-- Step 5 -->
  <circle cx='630' cy='60' r='45' fill='#FFFFFF' stroke='"&_DeliveredColor&"' />
    <g transform='translate(595, 30) scale(0.65)'>
  "&_DeliveredIcon&"
  </g>
  <text x='630' y='130' class='text' fill='"&_DeliveredColor&"'>Delivered</text>
  <text x='630' y='155' class='date'>"&_DeliveredDate&"</text>
  <text x='630' y='175' class='status'>"&_OrderStatus&"</text>
</svg>
"

RETURN _Svg
