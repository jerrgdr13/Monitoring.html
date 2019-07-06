# Monitoring.html
#monitoring purposes 
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="x-ua-compatible" content="ie=edge">
		<meta name="description" content="">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>MonitoringTool Production Monitoring</title>
		<link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />
		<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/7.0.0/normalize.min.css">
		<style>
			html, body { margin:0; padding:0; height:100%; }
			li { display:inline-block; margin-left:1em; margin-rigth:1em; }
			iframe { width:100%; height:103%; }
			#workspace { width:100%; height:885px; }
			.nav { padding:1px; line-height:0em; }
			.centered { text-align:center; }
			.top-nav { line-height:0em; background:whitesmoke; }
			.top-nav .active { padding:9px; background:gainsboro; }
			.sub-nav { line-height:0em; background:gainsboro; }
			.sub-nav .active { padding:9px; background:white; }
			.sub-nav .checkout .active { padding:9px; background:#00FFFF; }
		</style>
	</head>
	<body>
	
		<!--[if lte IE 9]>
			<p class="browserupgrade">You are using an <strong>outdated</strong> browser. Please upgrade your browser to improve your experience and security.</p>
		<![endif]-->
		
		<div class="content">
		
			<div id="top-nav" class="nav top-nav">
				<ul class="centered">
					<li><a href="javascript:void(0)">Loading top nav...</a></li>
				</ul>
			</div>
			
			<div id="sub-nav" class="nav sub-nav">
				<ul id="nav-home" class="centered">
					<li><a href="javascript:void(0)">Loading sub nav...</a></li>
				</ul>
			</div>
			
			<div id="workspace">
			</div>
		
		</div>
		
		<script src="https://code.jquery.com/jquery-3.2.1.min.js" integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4=" crossorigin="anonymous"></script>
		<script>
			
			var menu = [

				{
					label:  'Home',
					submenu: [
						{
							type:   'info',
							label:  'Top of MonitoringTool',
							url:    'https://MonitoringTool'
						},
						{
							type:   'info',
							label:  'System Status Summary',
							url:    'https://MonitoringTool'
						},
						{
							type:   'info',
							label:  'MonitoringTool Alarms',
							url:    'https://MonitoringTool',
						},
						{
							type:   'info',
							label:  'INFONAME',
							url:    'https://MonitoringTool',
						},
						{
							type:   'info',
							label:  'INFONAME',
							url:    'MonitoringTool',
						},
						{
							type:   'out',
							label:  'Last Link of the menu',
							url:    'http://MonitoringTool',
						}
					]
				},
				{
					label:  'Menu 2 (Any number of menues can be added with this same struture',
					submenu: [
						{
							type:   'info',
							label:  'INFONAME',
							url:    'https://MonitoringTool'
						},
						{
							type:   'info',
							label:  'INFONAME',
							url:    'https://MonitoringTool',
						},
						{
							type:   'checkout',
							label:  'INFONAME',
							url:    'https://MonitoringTool',
						},
						{
							type:   'checkout',
							label:  'INFONAME',
							url:    'https://MonitoringTool',
						}
					]
				}
			];

			function loadContent() {
				
				$('#workspace').append('<iframe id="tol" hidden="true" width="100%" height="100%" frameborder="0" src="http://MonitoringTool/"></iframe>');
				
				$('#tol').ready(function() {
					
					var topNav = '<ul class="centered">';
					var subNav = '<ul id="nav-home" class="centered">';
					var workspace = '';
					
					for (var i = 0; i < menu.length; i++) {
						
						topNav += '<li id="t' + i + '" class="' + menu[i].type + '"><a href="#" onclick="$(\'#sub-nav li:not(.reload)\').hide();$(\'#sub-nav li[id*=t' + i + 's]\').show();$(\'iframe:visible\').hide();$(\'iframe[id=t' + i + 'w0]\').show();$(\'.top-nav a\').removeClass(\'active\');$(this).addClass(\'active\');$(\'li[id$=s0] > a\').addClass(\'active\');$(\'.sub-nav a\').removeClass(\'active\');$(\'.sub-nav li[id$=s0] > a\').addClass(\'active\');">' + menu[i].label + '</a></li>';
						
						for (var j = 0; j < menu[i].submenu.length; j++) {
						
							if (menu[i].submenu[j].type == "out") {
							
								subNav += '<li id="t' + i + 's' + j + '" class="" hidden="true"><a href="' + menu[i].submenu[j].url + '" target="_blank" onclick="">' + menu[i].submenu[j].label + '</a></li>';
								continue;
							}
							
							subNav    += '<li id="t' + i + 's' + j + '" class="' + menu[i].submenu[j].type + '" hidden="true"><a href="#" onclick="$(\'iframe:visible\').hide();$(\'iframe[id*=t' + i + 'w' + j + ']\').show();$(\'.sub-nav a\').removeClass(\'active\');$(this).addClass(\'active\');">' + menu[i].submenu[j].label + '</a></li>';
							workspace += '<iframe id="t' + i + 'w' + j + '" hidden="true" width="100%" height="100%" frameborder="0" src="' + menu[i].submenu[j].url + '"></iframe>';
						}
						
					}
					
					topNav += '</ul>';
					subNav += '<li id="reload" class="reload"><a href="#" onclick="$(\'iframe:visible\')[0].src = $(\'iframe:visible\')[0].src;">&orarr;</a></li>';
					subNav += '</ul>';
					
					$('#top-nav').empty();
					$('#sub-nav').empty();
					$('#workspace').empty();
					
					$('#top-nav').append(topNav);
					$('#sub-nav').append(subNav);
					$('#workspace').append(workspace);
					
					$('#top-nav li a:first').addClass('active');
					$('#sub-nav li[id$=s0] a:first').addClass('active');
					
					$('#sub-nav li[id*=t0s]').show();
					$('#t0w0').show();
					
				});
				
			}
			
			$(document).ready(function() {
				loadContent();
			});
			
		</script>
	</body>
	
</html>
