# grunt-contrib-compass

首先先安装compass  

$npm install compass -g

创建compass工程

$compass create grunt-contrib-compass

项目结构

grunt-contrib-compass
 
     --.sass-cache

     --sass

     	--ie.scss

     	--print.scss

     	--screen.scss

     stylesheets

     	--ie.css

     	--print.css

     	--screen.css

    config.rb

可以在config里面看到如下文件

http_path = "/"  //基础路径

css_dir = "stylesheets"  // css路径

sass_dir = "sass"        //scss路径

images_dir = "images"    //img路径

javascripts_dir = "javascripts"   js路径

在文件根目录下在一次创建package.json和gruntfile.js文件

package.json

	{

	  "name": "grunt-contrib-compass",

	  "version": "0.0.1",

	  "description": "雪碧图",

	  "main": "Gruntfile.js",

	  "scripts": {

	    "test": "echo \"Error: no test specified\" && exit 1"

	  },

	  "author": "kimixue",

	  "license": "ISC",

	  "devDependencies": {

	    "devDependencies": {

		    "grunt": "~0.4.2",

		    "grunt-contrib-compass": "^1.0.3",

		    "grunt-contrib-connect": "^0.10.1",

		    "grunt-contrib-watch": "0.4.3",

		    "load-grunt-tasks": "^3.1.0",

            "time-grunt": "^1.2.1",

		    "grunt-sass": "0.6.1"

		  }

	  }

	}

gruntfile.js

	"use strict";

	module.exports = function(grunt) {

	  require('load-grunt-tasks')(grunt);

      require('time-grunt')(grunt);

	  grunt.initConfig({

	    pkg: grunt.file.readJSON('package.json'),

	    connect:{

	      options: {

	        port: 8080,
	        hostname: 'localhost', //默认就是这个值，可配置为本机某个 

	        livereload: 35729  //声明给 watch 监听的端口

	      },

	      server: {

	        options: {

	          open: true, //自动打开网页 http://

	          base: [
	            '.'  //主目录

	            ]

	          }

	        }
	      
	    },

	    watch: {

	      sass: {

	        files: ['sass/**/*.{scss,sass}','sass/_partials/**/*.{scss,sass}'],

	        tasks: ['compass']

	      },

	      livereload: {

	        options: {

	                  livereload:'<%=connect.options.livereload%>'

	                },

	                files:[  //下面文件的改变就会实时刷新网页

	                '*.html',

	                'stylesheets/{,*/}*.css',

	                'javascripts/{,*/}*.js',

	                'images/{,*/}*.{png,jpg}'

	          ]

	        }

	      },

	      compass: {

	       dist: {

	        options: {

	          config: 'config.rb'

	        }

	      }

	    }

	  });

	grunt.registerTask('default', ['compass:dist','connect:server', 'watch']);

	};


接下来在images下面创建icon文件夹 把要合并的png图片放进去

在scss文件夹创建icon.scss文件  设置如下

@charset "utf-8";

// 配置间距
$icon-spacing: 5px;


// 配置位置
$icon-position: 5px;

// 配置sprite的布局方式

$icon-layout: vertical;  // vertical/horizontal/diagonal/smart

// 自动输出尺寸

$icon-sprite-dimensions: true;

//

$icon-sprite-base-class: ".icon";

@import "compass/utilities/sprites";    // 加载compass sprites模块

@import "icon/*.png";                    // 导入icon目录下所有png图片

@include all-icon-sprites;                // 输出所有的雪碧图css


注意  具体设置  sass/icon.scss 里面有详细的说明



