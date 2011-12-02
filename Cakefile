path = require 'path'
{exec, spawn} = require 'child_process'
{puts, print} = require 'util'

code =
	lib: path.join __dirname, 'code/lib/'
	src: path.join __dirname, 'code/src/'
spec =
	lib: path.join __dirname, 'spec/lib/'
	src: path.join __dirname, 'spec/src/'

brew = (options) ->
	coffee = spawn 'coffee', options.split(' '), cwd: __dirname

	coffee.stdout.setEncoding 'utf8'
	coffee.stderr.setEncoding 'utf8'
	coffee.stdout.on 'data', (data) -> puts data.trim()
	coffee.stderr.on 'data', (data) -> puts "stderr: #{data.trim()}"

	coffee

task 'compile:code', ->
	puts "Cleanup lib (#{code.lib})."
	exec "rm -rf #{code.lib}*", ->
		puts "Compile src (#{code.src})."
		exec 'coffee -c -b -o code/lib/ code/src/', ->
			puts 'Code compiled!'

task 'compile:spec', ->
	puts "Cleanup lib (#{spec.lib})."
	exec "rm -rf #{spec.lib}*", ->
		puts "Compile src (#{spec.src})."
		exec 'coffee -c -b -o spec/lib/ spec/src/', ->
			puts 'Spec compiled!'

task 'watch:code', ->
	brew '-c -b -w -o code/lib/ code/src/'

task 'watch:spec', ->
	brew '-c -b -w -o spec/lib/ spec/src/'

task 'compile', ->
	invoke 'compile:code'
	invoke 'compile:spec'

task 'watch', ->
	invoke 'watch:code'
	invoke 'watch:spec'
