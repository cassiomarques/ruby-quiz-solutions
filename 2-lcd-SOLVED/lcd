#!/usr/bin/ruby
require 'optparse'

options_hash = {}
option_parser = OptionParser.new do |opts|
  opts.banner = "Usage: ruby lcd.rb [-s] <digits' size> <number to display>"

  opts.on("-s SIZE", Integer, "Specify the digits' size") do |size|
    options_hash[:size] = size
  end 
end

class Lcd
  ZERO  = [:line, :both_bars, :spaces, :both_bars, :line]
  ONE   = [:spaces, :right_bar, :spaces, :right_bar, :spaces]
  TWO   = [:line, :right_bar, :line, :left_bar, :line]
  THREE = [:line, :right_bar, :line, :right_bar, :line] 
  FOUR  = [:spaces, :both_bars, :line, :right_bar, :spaces]
  FIVE  = [:line, :left_bar, :line, :right_bar, :line]
  SIX   = [:line, :left_bar, :line, :both_bars, :line]
  SEVEN = [:line, :right_bar, :spaces, :right_bar, :spaces]
  EIGHT = [:line, :both_bars, :line, :both_bars, :line]
  NINE  = [:line, :both_bars, :line, :right_bar, :line]
  
  DIGITS = [ZERO, ONE, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE]
  
  def initialize(number, size)
    @number = number
    @size = (size ||= 2)
    @digits_array = @number.scan(/\d/).collect! { |d| d.to_i }
  end
      
  def print_number    
    puts [horizontals(0), verticals_array(1), horizontals(2), verticals_array(3), horizontals(4)].flatten.join("\n")
  end
      
  private
  def verticals_array(index)
    array = []
    @size.times { array << @digits_array.collect { |d| self.send(DIGITS[d][index]) }.join(" ") }
    array
  end
  
  def horizontals(index)
    @digits_array.collect { |d| self.send(DIGITS[d][index]) }.join(" ")
  end
  
  def left_bar
    line = "|"
    (@size + 1).times { |i| line << " " }
    line
  end
  
  def right_bar
    line = ""
    (@size + 1).times { |i| line << " " }
    line << "|"
  end
  
  def both_bars
    line = "|" 
    (@size).times { |i| line << " " }
    line << "|"
  end
  
  def line
    line = ""
    @size.times { |i| line << "-" }
    " #{line} "
  end
  
  def spaces
    line = ""
    (@size + 2).times { |i| line << " " }
    line
  end
end

option_parser.parse!(ARGV)
if ARGV.length == 0
  puts "You need to specify a number to be printed!"  
  exit()
end
lcd = Lcd.new(ARGV[0], options_hash[:size])
lcd.print_number
